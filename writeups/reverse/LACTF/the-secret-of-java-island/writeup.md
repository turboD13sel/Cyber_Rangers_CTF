# LACTF
## the-secret-of-java-island
**Task:** The Secret of Java Island is a 2024 point-and-click graphic adventure game developed and published by LA CTF Games. It takes place in a fictional version of Indonesia during the age of hacking. The player assumes the role of Benson Liu, a young man who dreams of becoming a hacker, and explores fictional flags while solving puzzles.
File: game.jar

**Solution:** First of all I decompiled the game.jar using [Decompiler](https://www.decompiler.com/). Got the source code for our game (JavaIsland.java). 
```
import java.awt.FlowLayout;
import java.awt.Font;
import java.net.Socket;
import java.security.MessageDigest;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Iterator;
import java.util.Scanner;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

class JavaIsland {
   private static JFrame frame = new JFrame();
   private static JLabel story = new JLabel();
   private static JButton button1 = new JButton();
   private static JButton button2 = new JButton();
   private static int state = 0;
   private static int prevState = 0;
   private static boolean hasGlove = false;
   private static String exploit = "";
   private static ArrayList<Integer> history = new ArrayList();

   private static void updateGame() {
      switch(state) {
      case 0:
         if (prevState == 2) {
            story.setText("<html>You want nothing to do with that lever and back away from it. The computer and lever still sit menacingly in the room.</html>");
         } else if (prevState == 1) {
            story.setText("<html>It's important to limit your screen time, or at least that's what your doctor told you. You back away from the computer. Surprisigly, the computer immediately turned off again after stepping away from it. The computer and lever still sit menacingly in the room.</html>");
         } else if (prevState == 6) {
            story.setText("<html>You run away from the hissing vent, but nothing seems to have happened. The computer and lever still sit menacingly in the room.</html>");
         } else {
            story.setText("<html>You wake up in a musty room with no lighting except a squeaky lamp hanging from the center of the ceiling. You remember nothing other than the fact that your name is Benson Liu and that you're on a quest to become the greatest hacker in the world. You look around the room and see a decrepit Dell workstation in the corner and a rusty lever on the opposite wall.</html>");
         }

         button1.setText("Inspect the computer");
         button2.setText("Inspect the lever");
         break;
      case 1:
         if (!hasGlove) {
            story.setText("<html>You walk up to the computer and reach for the power button. Before your hand even reaches the power button, the computer springs to life with a concerningly loud hum. The screen says \"WELCOME bliutech\" on it with a green button that says \"LOG IN\".</html>");
            button1.setText("Click the button");
            button2.setText("Back away");
         } else {
            story.setText("<html>While you're next to the computer, a distinct smell in the air makes you come to a realization: the hissing sound from the vent was from the release of toxic gas. Unfortunately, you realized this too late as you become light-headed before passing out. Game over.</html>");
            button1.setText("I understand");
            button2.setText("I understand");
         }
         break;
      case 2:
         story.setText("<html>As you walk closer to the lever you realize that it's completely covered in spider webs.</html>");
         button1.setText("Pull the lever");
         button2.setText("Back away");
         break;
      case 3:
         if (!hasGlove) {
            story.setText("<html>You reach for the lever, plunging your hand into the thick veil of spider webs. While trying to pull the lever, you feel a sharp pain on your arm before your vision fades to black. Game over.</html>");
            button1.setText("I understand");
            button2.setText("I understand");
         } else {
            story.setText("<html>You reach for the lever, plunging your gloved hand into the thick veil of spider webs. The lever makes a loud creaking sound as you press it down, powering a large floodlight that lights up the entire room. When you look at your hand in the newfound light, you see several large spiders climbing on your glove. Startled, you shake the glove off and run to the other corner of the room, where you see a flag that must've been there the entire time.</html>");
            button1.setText("Read the flag");
            button2.setText("Read the flag");
         }
         break;
      case 4:
         story.setText("<html>As soon as you click the button, a pair of handcuffs locks you to the table. There's no backing out now. The computer loads a website belong to X Enterprises: a multinational corporation that hates puppies! You have to hack them otherwise puppies all over the world will face the wrath of X Enterprises!</html>");
         button1.setText("Clobber the DOM");
         button2.setText("Pollute the prototype");
         break;
      case 5:
         try {
            Socket var0 = new Socket("chall.lac.tf", 31151);
            String var1 = "";

            int var3;
            for(Iterator var2 = history.iterator(); var2.hasNext(); var1 = var1 + var3) {
               var3 = (Integer)var2.next();
            }

            var0.getOutputStream().write((var1 + "\n").getBytes("UTF-8"));
            Scanner var5 = new Scanner(var0.getInputStream());
            String var6 = var5.nextLine();
            story.setText(var6);
            var5.close();
            var0.close();
         } catch (Exception var4) {
            System.err.println(var4.getMessage());
            story.setText("<html>The flag is garbled and unreadable. Contact an admin if you haven't done anything out of the ordinary.</html>");
         }

         button1.setText("Leave");
         button2.setText("Leave");
         break;
      case 6:
         story.setText("<html>As you submit the last exploit, X Enterprise's website goes down. You did it! You're officially the best and coolest hacker in the world. Your hand is released and a yellow kitchen glove is dropped from the ceiling and you put it on. As the computer shuts off and its loud humming comes to a halt, you can hear something quieter in the background: a soft hissing sound coming from the vent next to the computer.</html>");
         hasGlove = true;
         button1.setText("Run away");
... (107 lines left)
```
When we play the game, and we reach the stage where we need to hack the site, we need to enter the sequence or DOM or prototype. As a result, if the combination is correct (A string of 8 characters should be output, for example: "pdddppdd"), then we will get a flag. In the code, this combination is hashed by the SHA256 algorithm in the form of an array of bytes.
Byte array: {69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77}

I converted it to a user-friendly form: 4546af8bf66d0f1d13713d85d952f5de689e91092b23ed1634c984d3b8e960b3

I wrote python code to hash all possible combinations of "p" and "d" and output the result to notepad (hashing.py).

In the notepad, I found the same hash that I got after converting the byte array into a convenient form and got the correct combination: "dpddpdpp".

Entered this combination in game and got the flag:
