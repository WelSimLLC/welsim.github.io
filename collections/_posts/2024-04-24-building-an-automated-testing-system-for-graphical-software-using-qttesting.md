---
lang: en
layout: post
title:  "Building an automated testing system for graphical software using QtTesting"
date:   2024-04-24
author: "[SimLet](https://twitter.com/getwelsim)"
---

Automated testing is an essential component of modern large-scale software. High amounts of automated test cases are used to maintain the stability of large software products. For the software with a graphical user interface (GUI), establishing an automated testing system can be challenging due to limited resources. Previously, the author has written articles on automated testing for engineering simulation CAE software, see "[Automated Testing for General-Purpose Engineering Simulation CAE Software](https://welsim.com/2024/01/30/automated-testing-for-general-purpose-engineering-simulation-cae-software.html)", "[Quickly Create Regression Test Cases for WELSIM](https://welsim.com/2023/08/29/quickly-create-regression-test-cases-for-welsim.html)", and "[Automated Regression Testing for General-Purpose Engineering Simulation CAE Software](https://welsim.com/2023/08/22/automated-regression-testing-for-general-purpose-engineering-simulation-cae-software.html)". This article presents how to use QtTesting to quickly implement an automated testing system for graphical software from a software development perspective.
<p align="center">
  <img src="\assets\blog\20240424\welsim_qt_gui.png" alt="welsim_qt_gui" />
</p>


QtTesting is an open-source testing framework with a friendly license, similar to BSD3, and can be used for commercial products. It has been applied in practical instances for large-scale software such as VTK, ParaView, Slider3D, and WELSIM, proving to be an effective and user-friendly testing framework. As long as the software utilizes QT as its GUI framework, QtTesting can be used as the foundational component for the testing system. The source code of QtTesting can be directly downloaded from [https://gitlab.kitware.com/paraview/qttesting](https://gitlab.kitware.com/paraview/qttesting) or [https://github.com/Kitware/QtTesting](https://github.com/Kitware/QtTesting).


QtTesting is officially endorsed for UI testing. Although, in practical use, it not only can test GUI, but also can test any other functionalities of a product through the properties provided by the GUI, such as the accuracy of calculation results. Many of the numerical results in WELSIM can be validated through the functionality of QtTesting.
<p align="center">
  <img src="\assets\blog\20240424\welsim_qttesting_github.png" alt="welsim_qttesting_github" />
</p>


## QtTesting Framework

The Testing Module of QtTesting consists of two major modules: Translator and Player. Both modules establish connections with widgets in the QT framework to interact with the GUI framework. The translator captures events or signals of the widgets, while the player controls the widgets by traversing all active widgets to obtain the current object of the widget.

### Test Translator
The translator module provides users with a fast way to create test files, essentially acting as a macro command for mouse, keyboard, and widget controls. When users perform certain low-level Qt actions such as "mouse movement," "button press," "button release," etc., the generated signals will be captured and converted into higher-level events that can be serialized and played, such as "button activation." The pqWidgetEventTranslator class, and its derived classes play an important role in QtTesting. The derived classes of pqWidgetEventTranslator need to implement the translateEvent() method to handle Qt events and convert signals into high-level events consisting of two strings: a command and a command parameter (which may be empty). Finally, the high-level events are passed to their output container by emitting the recordEvent() signal once or multiple times. This is saved to an XML file, completing the recording of a macro command.
<p align="center">
  <img src="\assets\blog\20240424\pqWidgetEventTranslator.png" alt="pqWidgetEventTranslator" />
</p>


During program execution, pqEventTranslator receives every Qt event that occurs in the entire application runtime and sequentially passes Qt events to each pqWidgetEventTranslator instance. The high-level events emitted by pqEventTranslator can be captured by corresponding observers. Observers either serialize and print the high-level events, or save them. Currently, QtTesting includes two observers, pqEventObserverStdout and pqEventObserverXML, which serialize high-level events to standard screen output and XML files, respectively. Developers can also create their own observers to implement custom functions, such as serializing events to log files or Python scripts.
<p align="center">
  <img src="\assets\blog\20240424\welsim_regression_record.png" alt="welsim_regression_record" />
</p>


The translator module can also record check events, such as verifying a property. During the check, an overlay will be drawn on the widget where the mouse hovers. A green overlay indicates that the widget can be checked; if the overlay is red, it indicates otherwise. When clicking on the widget for checking, a check event will be recorded, and a related QString value will be output. This feature is a crucial part when verifying numerical results in WELSIM automated testing.
<p align="center">
  <img src="\assets\blog\20240424\welsim_regression_check.png" alt="welsim_regression_check" />
</p>


### Running Tests

The essence of running automated tests is to play back recorded macro commands. In the QtTesting framework, pqEventSource provides an abstract interface for objects that provide a stream of "high-level events." pqXMLEventSource inherits from pqEventSource and implements specific functionality. It is capable of reading XML files generated by pqEventObserverXML.
<p align="center">
  <img src="\assets\blog\20240424\welsim_regression_system_playback_ui.png" alt="welsim_regression_system_playback_ui" />
</p>


pqEventPlayer maintains a set of pqWidgetEventPlayer objects responsible for converting high-level events into low-level events. pqEventDispatcher retrieves events from pqEventSource and passes them to an instance of pqEventPlayer for execution. During runtime, each high-level event is encoded into three strings (object pointer, command, and parameters). Those are passed to pqEventPlayer::playEvent(). pqEventPlayer decodes the pointer address and uses it to locate the corresponding widget. Then, pqEventPlayer passes the high-level event and widget to each pqWidgetEventPlayer until one emits a signal indicating the event has been handled.
<p align="center">
  <img src="\assets\blog\20240424\pqWidgetEventPlayer.png" alt="pqWidgetEventPlayer" />
</p>


## Creating New Translators and Players


A new translator must at least reimplement the translateEvent(QObject object, QEvent event, int eventType, bool& error) method. First, it must check if the object is of the correct class. Then, it should handle the case of pqEventTypes::ACTION_EVENT, saving the command and related parameters. Sometimes it should also be able to handle pqEventTypes::CHECK_EVENT.

Similarly, a new player should at least reimplement the playEvent(QObject* object, const QString& command, const QString& arguments, int eventType, bool& error) method. First, it should handle pqEventTypes::ACTION_EVENT, converting the read command and parameters into Qt commands, returning true for events it can handle. For checking commands, it should be able to handle the pqEventTypes::CHECK_EVENT event type. Using the provided command and parameters to check the current value of the Qt object, it should set the error variable to false in case of different values, but it should return true for all handled check events, even failed ones.

Sometimes translator and player classes will correspond one-to-one. Developers can refer to pqLineEditEventTranslator and pqLineEditEventPlayer for simple examples, and pqAbstractItemViewEventTranslatorBase/pqAbstractItemViewEventPlayerBase for advanced examples.


## Running Tests
The source code of QtTesting is easy to compile, provided with a CMake program, which allows quick compilation into a static or dynamic library. Since this testing module is called in only a few places in the product, compilation into a static library is appropriate.

QtTesting has been successfully applied in software such as VTK, ParaView, but no test cases are available publicly. Fortunately, the general-purpose engineering simulation software WELSIM not only uses QtTesting as the GUI testing framework, but also open-sourced all test cases. Users can download WELSIM and the test cases to experience automated testing based on QtTesting.
<p align="center">
  <img src="\assets\blog\20240424\welsim_test_case_github.png" alt="welsim_test_case_github" />
</p>

WELSIM's automated testing user interface is based on the interface of QtTesting, with additional features, such as:
1. Support for reading *.wstb files, which contain a set of *.xml files, allowing for easier reading of multiple test cases at once.
2. Saving failed test cases to *.wstb files. Users do not need to manually select test cases for saving.
3. Adding a right-click context menu for selecting or deselecting test cases.
Developers can also add other functionalities as needed.


## Conclusion
QtTesting is a free testing system for Qt GUI frameworks. It not only provides the core functions for capturing QT events and signals, but also offers a user-friendly interface, making it friendly for both developers and end-users. QtTesting can assist software developers with quickly establishing testing systems. Its built-in functionality for capturing and controlling widgets can meet the testing needs of most products, and it is easy to adapt. Developers can add new testing modules based on the widgets of their own products.

We have successfully applied QtTesting to the automated testing of the simulation software WELSIM, achieving great results. The content discussed in this article can be applied not only to CAE simulation software, but also to any graphical software built using the QT framework.

---

<small>
WelSim and the author are not affiliated with Qt or QtTesting. There is no direct relationship between WelSim, the author, and the Qt or QtTesting development teams or organizations. The reference to Qt and QtTesting here is solely for technical blog articles and software usage reference.
</small>

