# LACTF
## the-secret-of-java-island
**Task:** The Secret of Java Island is a 2024 point-and-click graphic adventure game developed and published by LA CTF Games. It takes place in a fictional version of Indonesia during the age of hacking. The player assumes the role of Benson Liu, a young man who dreams of becoming a hacker, and explores fictional flags while solving puzzles.
File: game.jar

**Solution:** First of all I decompiled the game.jar using [Decompiler](https://www.decompiler.com/). Got the source code for our game (JavaIsland.java). 
```
Jesus
jesus_chr1st
Online

whiterobber — 01/14/2024 8:01 PM
UOFT CTF
Task: basic-overflow
My web developer friend said JavaScript is insecure so he made a password vault with CSS. Can you find the password to open the vault?

Wrap the flag in uoftctf{}

Make sure to use a browser that supports the CSS :has selector, such as Firefox 121+ or Chrome 105+. The challenge is verified to work for Firefox 121.0.

Solution:
Analyze CSS code:

/* LED1 /
         / b1_7_l1_c1 */
         .wrapper:has(.byte:nth-child(1) .latch:nth-child(7) .latchreset:active) .checker:nth-of-type(2) .checkerstate:nth-child(1) {
             transform: translateX(0%);
             transition: transform 0s;
         }

         .wrapper:has(.byte:nth-child(1) .latch:nth-child(7) .latchset:active) .checker:nth-of-type(2) .checkerstate:nth-child(1) {
             transform: translateX(-100%);
             transition: transform 0s;
         }

Pay attention to the first .wrapper.
If transform: translateX = (0%) then it means 1 (s).
If transform: translateX = (100%) then it means 0 (r).

Screenshots solution are attached below:
https://prnt.sc/bHH_aQcaPAlN
https://prnt.sc/G6-C33usloRE
https://prnt.sc/H7mbwZRH2t_g

Then rewrite the values and get the following:
01000011-01110011-01010011-01011111-01101100-00110000-01100111-00110001-01100011-01011111-01101001-01110011-01011111-01100110-01110101-01101110-01011111-00110011-01101000

Translate this data into ASCII and get the flag: uoftctf{CsS_l0g1c_is_fun_3h} 
Source file: 
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
... (72 KB left)
Expand
css-password.html
122 KB
turboD13sel — 01/20/2024 6:43 PM
#include <stdio.h>

int Welcome, to, MAPNA, CTF, Year_2k24;

int main() {
    const char* code = "Welcome,to,MAPNA,CTF,Year_2k24;main(){for(++CTF;to=-~getchar();Welcome+=11==to,Year_2k24++)CTF=to>0xe^012>to&&'`'^to^65?!to:!CTF?++MAPNA:CTF;printf(\"MAPNA{%4d__%d__%d_!}\\n\",(to+20)^(Welcome+24)+1390,MAPNA+=(!CTF&&Year_2k24)+10,Year_2k24+31337);}";

    for (int i = 0; code[i] != '\0'; i++) {
        to = code[i];
        Welcome += 11 == to;
        CTF = to > 0xe ^ 012 > to && '`' ^ to ^ 65 ? !to : !CTF ? ++MAPNA : CTF;
        Year_2k24++;
    }

    printf("Year_2k24: %d\n", Year_2k24);  // Вивід Year_2k24 перед основним принтом
    printf("MAPNA{%4d__%d__%d_!}\n", (to + 20) ^ (Welcome + 24) + 1390, MAPNA += (!CTF && Year_2k24) + 10, Year_2k24 + 31337);

    return 0;
}
 
Image
gcc -o mapna_ctf mapna_ctf.c
./mapna_ctf mapna_ctf.c
turboD13sel — 01/20/2024 8:01 PM
MAPNA{13031531582_!}
Image
Image
whiterobber — 02/09/2024 4:07 PM
Attachment file type: unknown
token_validation
14.16 KB
Attachment file type: unknown
easylogin
14.19 KB
turboD13sel — 02/09/2024 4:34 PM
for part1 in range(1000000):  # Iterate through all possible 6-digit numbers
        for part2 in range(1000000):
            token = [part1, part2]
            FUN00101159(token, param_2)
            if token[0] == expected_token_part1 and token[1] == expected_token_part2:
                return f"Token found: {part1:06d}{part2:06d}"
turboD13sel — 02/15/2024 10:01 PM
BITSCTF
baby-rev
Given file (baby-rev). Just decompile it with ghidra. We can se func "myfunc" where input string compares to each symbol. 
BITSCTF{w3lc0me_t0_r3v} 
Attachment file type: unknown
baby-rev
15.86 KB
m1n3 — 02/15/2024 11:28 PM
did u guys
solve it?
XTO_9I? — 02/15/2024 11:28 PM
Yes, there's a flag
turboD13sel — 02/18/2024 12:11 AM
BITSCTF
Touch Grass
https://medium.com/@mohammadolimat/bitsctf-2024-reverse-writeup-0f15f28c342f
Medium
BITSCTF 2024 Reverse Writeup
بسم الله الرحمن الرحيم
turboD13sel — 02/18/2024 12:41 PM
LACTF
rev/aplet321
Task: Unlike Aplet123, Aplet321 might give you the flag if you beg him enough.
nc chall.lac.tf 31321
File: aplet321

Solution: Decompile the file with ghidra. We can see the main function.

The program checks the number of entered words "pretty" and "please" and counts them. Then follows the condition where:
the sum of the words "pretty" and "please" should be 54 and their difference -24.

By easy metamatic calculations, we will get that the number of words "pretty" should be 15 and "please" should be 39. There should also be a word flag at the end. Here is the final line we must enter:
please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please please pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty pretty flag
Enter and get the flag: lactf{next_year_i'll_make_aplet456_hqp3c1a7bip5bmnc}
Attachment file type: unknown
aplet321
15.96 KB
turboD13sel — 02/18/2024 3:36 PM
Need help, i am on half way to get solution.
Part of java code:
private static String exploit = "";

if (exploit.length() == 8) {
            try {
               MessageDigest var1 = MessageDigest.getInstance("SHA-256");
               if (!Arrays.equals(var1.digest(exploit.getBytes("UTF-8")), new byte[]{69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77})) {
                  state = 7;
               } else {
                  state = 6;
               }

               updateGame();
            } catch (Exception var2) {
               throw new RuntimeException(var2);
            }
         }

I need to get the value of the exploit so that it satisfies the condition and get state = 6.

exploit should be size 8 
turboD13sel — 02/18/2024 4:33 PM
Забийте, я зробив
turboD13sel — 02/18/2024 4:46 PM
LACTF
rev/the-secret-of-java-island
Task: The Secret of Java Island is a 2024 point-and-click graphic adventure game developed and published by LA CTF Games. It takes place in a fictional version of Indonesia during the age of hacking. The player assumes the role of Benson Liu, a young man who dreams of becoming a hacker, and explores fictional flags while solving puzzles.
File: game.jar

Solution: First of all I decompiled the game.jar using https://www.decompiler.com/. Got the source code for our game (JavaIsland.java). When we play the game, and we reach the stage where we need to hack the site, we need to enter the sequence or DOM or prototype. As a result, if the combination is correct (A string of 8 characters should be output, for example: "pdddppdd"), then we will get a flag. In the code, this combination is hashed by the SHA256 algorithm in the form of an array of bytes.
Byte array: {69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77}

I converted it to a user-friendly form: 4546af8bf66d0f1d13713d85d952f5de689e91092b23ed1634c984d3b8e960b3

I wrote python code to hash all possible combinations of "p" and "d" and output the result to notepad (hashing.py).

In the notepad, I found the same hash that I got after converting the byte array into a convenient form and got the correct combination: "dpddpdpp".

Entered this combination in game and got the flag:
Image
Attachment file type: unknown
game.jar
5.32 KB
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
Collapse
JavaIsland.java
10 KB
import hashlib

def generate_combinations(length):
    combinations = []
    generate_combinations_helper("", length, combinations)
    return combinations
Expand
hashing.py
2 KB
Java decompiler online / APK decompiler - Decompiler.com
Online decompiler for Java, Android, Python and C#.
turboD13sel — 02/24/2024 3:46 PM
@m1n3 How you solve rev? Which tool u use to decompile exe file?
m1n3 — 02/24/2024 3:48 PM
heyy
i  just decompiled it into pseudocode
turboD13sel — 02/24/2024 3:51 PM
forget, iam stupid 
i thinked it wasnt password 
and even dont tried to enter it
m1n3 — 02/24/2024 3:52 PM
ida
i just used ida
turboD13sel — 02/24/2024 3:52 PM
also
m1n3 — 02/24/2024 5:44 PM
@turboD13sel hey bro\
about pwn
i can send flag here
if u want
did yall do any others?
turboD13sel — 02/24/2024 5:45 PM
want to know how to do this chall
m1n3 — 02/24/2024 5:47 PM
did u do the reverse one
PIN
turboD13sel — 02/24/2024 5:47 PM
yes
m1n3 — 02/24/2024 5:47 PM
also here is it
Image
just simple BOF
xd
turboD13sel — 02/24/2024 5:47 PM
hahahahahahah
oh fuck
093
ppin
also decompiled with ida, and calculated xor
m1n3 — 02/24/2024 5:49 PM
just that?
turboD13sel — 02/24/2024 5:52 PM
yes
you can see waht pin must be 3 digit. After XOR calculations it must equal to SCC
i get second numbers which used in xor calculations. you just click on them in ida
1 - 63h
2 - 7A
3 - 70
its in hex
and i just took over digits
m1n3 — 02/24/2024 5:54 PM
oh nice
ur pretty good bro
turboD13sel — 02/24/2024 5:55 PM
0 xor 63 = S
etc ..
m1n3 — 02/24/2024 5:56 PM
so how can i get
that flag?
with 093 pin?
turboD13sel — 02/24/2024 5:56 PM
PIN: 093
yes
m1n3 — 02/24/2024 5:56 PM
ohoh
ok sry
ill try to finish last misc
its kinda
turboD13sel — 02/24/2024 5:56 PM
run in cmd
pin.exe 093
m1n3 — 02/24/2024 5:56 PM
like it works but drops the requests after 2nd round
for some reason
m1n3 — 02/24/2024 5:57 PM
nice one bro
﻿
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
         button2.setText("Investigate");
         break;
      case 7:
         story.setText("<html>Your hacking was ineffective, and the firewall in front of X Enterprises has detected malicious activity and IP banned you. You are not the hacker that you wanted to be, and promptly collapse to the ground with grief. Game over.</html>");
         button1.setText("I understand");
         button2.setText("I understand");
      }

   }

   private static void transitionState(int var0) {
      history.add(var0);
      prevState = state;
      switch(state) {
      case 0:
         if (var0 == 0) {
            state = 1;
         } else {
            state = 2;
         }
         break;
      case 1:
         if (hasGlove) {
            System.exit(0);
         } else if (var0 == 0) {
            state = 4;
         } else {
            state = 0;
         }
         break;
      case 2:
         if (var0 == 0) {
            state = 3;
         } else {
            state = 0;
         }
         break;
      case 3:
         if (!hasGlove) {
            System.exit(0);
         } else {
            state = 5;
         }
         break;
      case 4:
         if (var0 == 0) {
            exploit = exploit + "d";
            story.setText("You clobbered the DOM. That was exploit #" + exploit.length() + ".");
         } else {
            exploit = exploit + "p";
            story.setText("You polluted the prototype. That was exploit #" + exploit.length() + ".");
         }

         if (exploit.length() == 8) {
            try {
               MessageDigest var1 = MessageDigest.getInstance("SHA-256");
               if (!Arrays.equals(var1.digest(exploit.getBytes("UTF-8")), new byte[]{69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77})) {
                  state = 7;
               } else {
                  state = 6;
               }

               updateGame();
            } catch (Exception var2) {
               throw new RuntimeException(var2);
            }
         }
         return;
      case 5:
      case 7:
         System.exit(0);
         break;
      case 6:
         if (var0 == 0) {
            state = 0;
         } else {
            state = 1;
         }
      }

      updateGame();
   }

   public static void main(String[] var0) {
      frame.setDefaultCloseOperation(3);
      frame.setSize(500, 500);
      Font var1 = new Font("sans-serif", 0, 24);
      JPanel var2 = new JPanel();
      story.setFont(var1);
      button1.setFont(var1);
      button2.setFont(var1);
      var2.setLayout(new FlowLayout());
      var2.add(button1);
      var2.add(button2);
      button1.addActionListener((var0x) -> {
         transitionState(0);
      });
      button2.addActionListener((var0x) -> {
         transitionState(1);
      });
      frame.getContentPane().add("Center", story);
      frame.getContentPane().add("South", var2);
      updateGame();
      frame.setVisible(true);
   }
}
JavaIsland.java
10 KB
```
When we play the game, and we reach the stage where we need to hack the site, we need to enter the sequence or DOM or prototype. As a result, if the combination is correct (A string of 8 characters should be output, for example: "pdddppdd"), then we will get a flag. In the code, this combination is hashed by the SHA256 algorithm in the form of an array of bytes.

Byte array: {69, 70, -81, -117, -10, 109, 15, 29, 19, 113, 61, -123, -39, 82, -11, -34, 104, -98, -111, 9, 43, 35, -19, 22, 52, -55, -124, -45, -72, -23, 96, -77}

I converted it to a user-friendly form: 4546af8bf66d0f1d13713d85d952f5de689e91092b23ed1634c984d3b8e960b3

I wrote python code to hash all possible combinations of "p" and "d" and output the result to notepad:

```
import hashlib

def generate_combinations(length):
    combinations = []
    generate_combinations_helper("", length, combinations)
    return combinations

def generate_combinations_helper(prefix, length, combinations):
    if length == 0:
        combinations.append(prefix)
        return
    generate_combinations_helper(prefix + "d", length - 1, combinations)
    generate_combinations_helper(prefix + "p", length - 1, combinations)

def calculate_sha256_hash(string):
    return hashlib.sha256(string.encode()).hexdigest()

def write_to_file(combinations, filename):
    with open(filename, "w") as file:
        for combination in combinations:
            hash_value = calculate_sha256_hash(combination)
            file.write(f"{combination}, {hash_value}\n")

if __name__ == "__main__":
    length = 8
    filename = "combinations_with_hashes.txt"
    combinations = generate_combinations(length)
    write_to_file(combinations, filename)
    print("Combinations with hashes generated and written to", filename)
```

In the notepad, I found the same hash that I got after converting the byte array into a convenient form and got the correct combination: "dpddpdpp".

Entered this combination in game and got the flag:
[flag](image.png)
