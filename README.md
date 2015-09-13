# Main
+public class CommandParser {
+
+    public static void printHeader() {
+        System.out.println("Command line parser, powered by Polina Sytnik (C) 2015");
+        System.out.println();
+    }
+
+    private static void printHelp() {
+        System.out.println("use CommandParser.exe /? to see set of allowed commands");
+    }
+
+    private static void printHelpExt() {
+        System.out.println("CommandParser.exe [/?] [/help] [-help] [-k key value] [-ping] [-print <print a value>]");
+    }
+
+
+    private static void printMessage(String arg) {
+        System.out.println("Message: " + arg);
+    }
+
+    private static void printBeep() {
+        Toolkit.getDefaultToolkit().beep();
+        System.out.println("Be-e-e-e-e-p!!!!");
+    }
+
+    private static void printKeyValueTable(String[] args, int i) {
+        for (int j = i + 1; j < args.length; j += 2) {
+            if (isParameter(args[j])) return;
+
+            System.out.print(args[j] + " - ");
+
+            if (j + 1 < args.length && !isParameter(args[j + 1]))
+                System.out.println(args[j + 1]);
+            else
+                System.out.println("<null>");
+        }
+    }
+
+    private static boolean isParameter(String string) {
+        return string.equals("-ping")
+                || string.equals("-print")
+                || string.equals("/?")
+                || string.equals("/help")
+                || string.equals("-help");
+    }
+
+    public static void performParsing(String[] args) {
+
+        if (args.length == 0 || args[0].equals("")) {
+            printHelp();
+            return;
+        }
+
+        for (int i = 0; i < args.length; i++) {
+            if (args[i].equals("/?") || args[i].equals("/help") || args[i].equals("-help")) {
+                printHelpExt();
+                continue;
+            }
+            if (args[i].equals("-print")) {
+                printMessage(args[i + 1]);
+                continue;
+            }
+            if (args[i].equals("-ping")) {
+                printBeep();
+                continue;
+            }
+            if (args[i].equals("-k")) {
+                printKeyValueTable(args, i);
+            }
+        }
+
+    }
+}

+  public static void main(String[] args) {
+        Scanner input = new Scanner(System.in);
+        CommandParser.printHeader();
+
+        for (; ; ) {
+            String string = input.nextLine();
+
+            if (string.equals("-exit")) {
+                exit(input);
+                return;
+            }
+
+            CommandParser.performParsing(string.split("\\s"));
+        }
+    }
+
+    private static void exit(Scanner input) {
+        System.out.println("Bye!");
+        input.close();
+    }
+}
