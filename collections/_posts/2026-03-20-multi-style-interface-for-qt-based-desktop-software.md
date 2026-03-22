---
lang: en
layout: post
title:  "Multi-style interface for Qt-based desktop software"
date:   2026-03-20
author: "[SimLet](https://twitter.com/getwelsim)"
---

Qt is one of the most popular cross-platform C++ Graphical User Interface (GUI) application frameworks in the world. Its most powerful feature is its cross-platform capability: developers write code once and, after recompilation, are able to run it on desktop (Windows, macOS, Linux), mobile (iOS, Android), and embedded systems (QNX, VxWorks, various RTOS). Software products, particularly large-scale industrial software, are frequently built on the Qt framework. From a developer perspective, this article discusses how to optimally implement multi-theme interfaces in Qt software, focusing on Dark theme.
<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_theme_dark.png" alt="welsim_qt_theme_dark" />
</p>

In regards to the development of large-scale Qt desktop applications, such as IDEs, industrial control software, or productivity tools, the UI is more than just aesthetics; it concerns operational comfort during long usage sessions, the clarity of information hierarchy, and brand professionalism. As a result, modern large-scale visualization software support multiple interface styles, commonly categorized into Light and Dark themes. Because Light mode is typically the default, Dark mode requires dedicated functional implementation by developers. From a practical standpoint, just these two styles are generally sufficient for most needs.


## Implementation methods
There are several established solutions for implementing and dynamically switching between themes in Qt. This article focuses on the two most common methods: **Source Code** and **QSS files**.
<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_theme_options.png" alt="welsim_qt_theme_options" />
</p>

### Setting QStyle in C++/Python Source Code
This is the classic approach. Developers define different themes directly in the source code, with customized colors for each theme, and apply the themes to the QApplication via the setStyle and setPalette functions. The advantage of this method is its simplicity, speed, and ease of maintenance as developers manage styles alongside other Qt code. However, because user-defined styles require access to the source code, this technique has weak scalability. For large commercial software, especially engineering software, users rarely customize interface styles anyways, making direct QStyle configuration in source code an efficient solution. The general-purpose engineering simulation software WELSIM also adopts this approach.


### Setting QStyleSheet via QSS
This is a more flexible and adaptable method, implemented by loading different .qss files combined with variable substitution (using regular expressions or setProperty). One advantage is the seperation of the style from the application functionality as style modifications do not require recompiling the source code, and end-users can modify or add QSS files to achieve custom styles. The drawbacks include slightly reduced rendering performance for complex interfaces and a relatively cumbersome development and maintenance process that requires a proficiency in QSS syntax.


## Light Theme vs. Dark Theme
Light and dark are the two primary color schemes for multi-style development. The light style is similar to the operating system's native display, so the main task in developing a multi-theme interface is implementing the dark theme. These two themes can be switched on demand, much like the map system in a car's central display where it's a light background during the day and dark background at night. Dark-themed desktop software is becoming increasingly popular because it is eye-friendly, For users of large-scale engineering software who spend extended periods viewing screens, dark interfaces effectively reduce eye strain.
<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_chart_light_dark.png" alt="welsim_qt_chart_light_dark" />
</p>

Many developers mistakenly believe dark mode is a simple color inversion. In reality, directly flipping white background/black text to black background/white text causes visual fatigue due to extreme contrast and a halo effect. Below are the recommended color schemes for light and dark themes:

### Dark Theme
**Background**: Avoid pure black (#000000); use dark gray (e.g., #121212 or #1E1E1E) for depth through shadows.
**Layout**: Follow the "lighter is closer" principle for persepective. The base background is darkest, while pop-ups or floating panels should be slightly lighter.
**Text**: Avoid pure white (#FFFFFF); use off-white or light gray (e.g., #E0E0E0) to reduce glare.

### Light Theme
**Background**: Choose a very light gray (e.g., #F5F5F5) as the primary background, reserving pure white for editing or core content areas.
**Contrast**: Use subtle borders rather than large shadows to distinguish modules.
**Color Balance**: Ensure accent colors (status bars, icons) have enough saturation to remain visible under bright light.

Notably, Qt's built-in Fusion style is an excellent base theme with built-in light and dark variants; developers can directly use Fusion as a development template.

## Icons
Background color changes may render existing icons incompatible (e.g., icons designed for light themes become lose contrast on dark backgrounds). Qt provides solutions for multi-style icons, with three common methods:
1. Using QStyle Standard Icons
Automatically adapts to light/dark themes in Fusion mode - the most convenient option. However, Qt's built-in standard icons are limited and only sufficient for small software; large applications require custom icons.
2. Dynamic SVG Color Changing
Replace fixed colors (e.g., fill="#000000") in SVG icons with fill="currentColor". Qt automatically replaces currentColor with the widget's foreground color (palette.color(QPalette::WindowText)). This only works for single-color icons; multi-color icons cannot achieve ideal results.
3. Dual Icon Sets (Light + Dark)
The standard for large software. Despite needing to create and maintain two icon sets, it is the most efficient method, supporting complex and high-quality icons. This is the approach used for icons in WELSIM's light and dark styles.

<p align="center">
  <img src="\assets\blog\20260320\welsim_icons_light_dark.png" alt="welsim_icons_light_dark" />
</p>

When using two sets of icon themes, determine whether the application's current theme is dark. If it is, apply the dark icons; otherwise, use the light icons. There are several ways to detect a dark theme; for Qt 6.5 and above, you can use the following method:

``
bool isDark() { 
   return qApp->styleHints()->colorScheme() == Qt::ColorScheme::Dark; 
}
``

Dynamically load icons in updateIcon() function.

```
void updateIcon() { 
 QString path = isDark() ? ":/icons/icon_dark.svg" : ":/icons/icon_light.svg"; 
 ui->button->setIcon(QIcon(path)); 
}
```

Place updateIcon() in the changeEvent(QEvent *e) slot function. Capture system theme changes via e->type() == QEvent::PaletteChange or e->type() == QEvent::StyleChange.

## OpenGL Rendering Widgets
Many large applications include OpenGL-based rendering widgets where Qt's default QWidget theme settings do not automatically apply. Manual synchronization is required:
Set the renderer's background color to match the QWidget background.
Configure canvas background and drawing colors.

<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_chart_light_dark.png" alt="welsim_qt_chart_light_dark" />
</p>

Taking a VTK-implemented chart as an example, synchronizing the 2D plotting area requires setting the renderer background, chart background, and axis colors, then updating the renderer.

The source code for theme synchronization is shown below.

```
void myWelSimChartPlot::syncVtkThemeWithQtDark(QWidget* qtWidget)
{
   vtkRenderWindow* renderWindow = this->renderWindow();
   vtkRendererCollection* renderers = renderWindow ? renderWindow->GetRenderers() : nullptr;
   vtkRenderer* renderer = renderers ? renderers->GetFirstRenderer() : nullptr;
   if (!qtWidget || !renderer || !renderWindow) return;
   const QPalette palette = qtWidget->palette();
   const QColor bgColor = palette.color(QPalette::Base);
   const QColor fgColor = palette.color(QPalette::WindowText);
   renderer->SetBackground(qColorToVtk(bgColor));
   vtkColor4ub color;
   color.Set(bgColor.red(), bgColor.green(), bgColor.blue(), bgColor.alpha());
   this->chart()->GetBackgroundBrush()->SetColor(color);
   int axisIDs[4] = { vtkAxis::BOTTOM, vtkAxis::TOP, vtkAxis::LEFT, vtkAxis::RIGHT };
   for (unsigned int axisIndex = 0; axisIndex < 4; ++axisIndex)
   {
     int axisID = axisIDs[axisIndex];
     vtkAxis* axis = this->chart()->GetAxis(axisID);
     if (!axis) { assert(0); continue; }
     axis->GetTitleProperties()->SetColor(qColorToVtk(fgColor));
     axis->GetLabelProperties()->SetColor(qColorToVtk(fgColor));
     axis->GetGridPen()->SetColorF(qColorToVtk(borderColor));
     axis->GetPen()->SetColorF(qColorToVtk(fgColor));
   }
   renderWindow->Render();
}
```

In addition to the 2D drawing window, OpenGL-driven 3D windows can also be configured with corresponding color themes. However, in actual product design, this is often unnecessary because 3D windows provide their own color schemes. As shown in the figure, WELSIM's 3D rendering window supports three background options: blue-white gradient, black, and white. Users can customize the style and color of the 3D OpenGL rendering window to fit their needs.

<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_3dview_dark.png" alt="welsim_qt_3dview_dark" />
</p>
<p align="center">
  <img src="\assets\blog\20260320\welsim_qt_3dview_light.png" alt="welsim_qt_3dview_light" />
</p>


## Conclusion
Nowadays, for any well-established large-scale engineering software, supporting multiple themes has become an essential feature. At the very least, the software should include both Light and Dark modes. The core challenge lies in the implementation of the Dark theme because although the technical difficulty is not necessarily high, it involves a vast amount of meticulous development and testing. This takes significant development time as well as long-term optimization and maintenance. If the existing codebase contains local style modifications, such as setStyle or setStyleSheet functions, they must be updated accordingly. From a maintenance perspective, it is best to remove those local styling snippets and instead allow a global style manager to govern the entire software interface.


---
*WELSIM and its author are not affiliated with Qt or the Qt development team/organization. All open-source software names and images referenced herein are for technical blog and software usage reference only.*


