# Re-produce demo

- Step 1、git clone the repo. open jmx file.

```shell
mvn jmeter:configure jmeter:gui -DguiTestFile=src/test/jmeter/Chinese_Plan.jmx
```

- Step 2、edit HTTP Request Body Dada text area in (中文线程组) Thread Group. type some Chinese characters and save.

![type some Chinese characters](./20221206205121.jpg)

and then, Jmeter GUI be suspended, I can't do anything. The log file ([target/jmeter/logs/Chinese_Plan.log](./Chinese_Plan.jmx.log)) can not find any helpful information.

## Re-produce machine info

- os.name=Mac OS X
- os.arch=x86_64
- Apache Maven 3.8.2 (ea98e05a04480131370aa0c110b8c54cf726c06f)
- java.version=11.0.17, [download links](https://www.azul.com/downloads/?version=java-11-lts&os=macos&architecture=x86-64-bit&package=jdk-fx)


---

But, if I start jmeter gui by this way and typing chinese characters. Jmeter GUI would not be suspended.

```shell
cd target/55123e3c-0a16-44eb-b68e-a0cc44002e02/jmeter/bin

java -Xms5120M -Xmx6144M -server -XX:+HeapDumpOnOutOfMemoryError -XX:MaxMetaspaceSize=256m -XX:+UseG1GC -XX:MaxGCPauseMillis=100 -XX:G1ReservePercent=20 -jar ApacheJMeter-5.4.1.jar -d /Users/yeshan/works/aligame-tc-qa/reproduce_demo/target/55123e3c-0a16-44eb-b68e-a0cc44002e02/jmeter -j /Users/yeshan/works/aligame-tc-qa/reproduce_demo/target/jmeter/logs/Chinese_Plan.jmx.log -l /Users/yeshan/works/aligame-tc-qa/reproduce_demo/target/test/jmeter/results/2022-1206-210954-512-Chinese_Plan.jtl -t /Users/yeshan/works/aligame-tc-qa/reproduce_demo/src/test/jmeter/Chinese_Plan.jmx
```

But got this Exception:

```shell
javax.swing.text.BadLocationException: Position not represented by view
        at org.fife.ui.rsyntaxtextarea.WrappedSyntaxView.modelToView(WrappedSyntaxView.java:770)
        at org.fife.ui.rsyntaxtextarea.WrappedSyntaxView.yForLineContaining(WrappedSyntaxView.java:1130)
        at org.fife.ui.rsyntaxtextarea.RSyntaxTextAreaUI.yForLineContaining(RSyntaxTextAreaUI.java:263)
        at org.fife.ui.rtextarea.RTextAreaBase.yForLineContaining(RTextAreaBase.java:1216)
        at org.fife.ui.rtextarea.LineNumberList$Listener.caretUpdate(LineNumberList.java:700)
        at java.desktop/javax.swing.text.JTextComponent.fireCaretUpdate(JTextComponent.java:412)
        at org.fife.ui.rtextarea.RTextArea.fireCaretUpdate(RTextArea.java:629)
        at org.fife.ui.rsyntaxtextarea.RSyntaxTextArea.fireCaretUpdate(RSyntaxTextArea.java:873)
        at java.desktop/javax.swing.text.JTextComponent$MutableCaretEvent.fire(JTextComponent.java:4489)
        at java.desktop/javax.swing.text.JTextComponent$MutableCaretEvent.stateChanged(JTextComponent.java:4511)
        at java.desktop/javax.swing.text.DefaultCaret.fireStateChanged(DefaultCaret.java:812)
        at java.desktop/javax.swing.text.DefaultCaret.changeCaretPosition(DefaultCaret.java:1283)
        at java.desktop/javax.swing.text.DefaultCaret.handleSetDot(DefaultCaret.java:1182)
        at java.desktop/javax.swing.text.DefaultCaret$DefaultFilterBypass.setDot(DefaultCaret.java:1947)
        at java.desktop/javax.swing.text.NavigationFilter.setDot(NavigationFilter.java:64)
        at org.fife.ui.rtextarea.ConfigurableCaret$FoldAwareNavigationFilter.setDot(ConfigurableCaret.java:724)
        at java.desktop/javax.swing.text.DefaultCaret.setDot(DefaultCaret.java:1160)
        at java.desktop/javax.swing.text.DefaultCaret$Handler.insertUpdate(DefaultCaret.java:1757)
        at java.desktop/javax.swing.text.AbstractDocument.fireInsertUpdate(AbstractDocument.java:203)
        at org.fife.ui.rsyntaxtextarea.RSyntaxDocument.fireInsertUpdate(RSyntaxDocument.java:187)
        at java.desktop/javax.swing.text.AbstractDocument.handleInsertString(AbstractDocument.java:757)
        at java.desktop/javax.swing.text.AbstractDocument.insertString(AbstractDocument.java:716)
        at java.desktop/javax.swing.text.PlainDocument.insertString(PlainDocument.java:131)
        at java.desktop/javax.swing.text.AbstractDocument.replace(AbstractDocument.java:675)
        at java.desktop/javax.swing.text.JTextComponent.setText(JTextComponent.java:1729)
        at org.apache.jmeter.gui.util.JSyntaxTextArea.setInitialText(JSyntaxTextArea.java:293)
        at org.apache.jmeter.protocol.http.config.gui.UrlConfigGui.configure(UrlConfigGui.java:279)
        at org.apache.jmeter.protocol.http.control.gui.HttpTestSampleGui.configure(HttpTestSampleGui.java:96)
        at org.apache.jmeter.gui.GuiPackage.refreshCurrentGui(GuiPackage.java:468)
        at org.apache.jmeter.gui.GuiPackage.updateCurrentGui(GuiPackage.java:452)
        at org.apache.jmeter.gui.action.Save.doAction(Save.java:175)
        at org.apache.jmeter.gui.action.ActionRouter.performAction(ActionRouter.java:87)
        at org.apache.jmeter.gui.action.ActionRouter.lambda$actionPerformed$0(ActionRouter.java:69)
        at java.desktop/java.awt.event.InvocationEvent.dispatch(InvocationEvent.java:313)
        at java.desktop/java.awt.EventQueue.dispatchEventImpl(EventQueue.java:770)
        at java.desktop/java.awt.EventQueue$4.run(EventQueue.java:721)
        at java.desktop/java.awt.EventQueue$4.run(EventQueue.java:715)
        at java.base/java.security.AccessController.doPrivileged(Native Method)
        at java.base/java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(ProtectionDomain.java:85)
        at java.desktop/java.awt.EventQueue.dispatchEvent(EventQueue.java:740)
        at java.desktop/java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:203)
        at java.desktop/java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:124)
        at java.desktop/java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:113)
        at java.desktop/java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:109)
        at java.desktop/java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:101)
        at java.desktop/java.awt.EventDispatchThread.run(EventDispatchThread.java:90)
```