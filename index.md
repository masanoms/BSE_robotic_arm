# Three-Jointed Robotic Arm

I chose to build a robotic arm because I wanted a project that combined mechanical design, electronics, and programming. I also plan to study engineering, So I thought it would be a good way to learn how motors, Control systems, and software all work together to help make the robotic arm come to life and how 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Malakai.C | Wahi high school | Aerospace engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="[https://www.youtube.com/embed/F7M7imOVGug](https://www.youtube.com/watch?v=Pb9fzQlkjnU)" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/Pb9fzQlkjnU?si=VB-x9pcSFJBav_JV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my first milestone in the BlueStamp Engineering Remote Program, I completed the base version of my Arduino robotic arm and after I completed the assembly I focused on making the code for the robotic arm so that when I move the joysticks that it can move around. 

The robot consists of four servo motors that provide movement at the base, shoulder, elbow, and gripper joints. Each servo is controlled using two joystick modules, allowing the arm to move smoothly in real time. The joystick modules output analog voltage signals that the Arduino reads through its analog input pins. The Arduino then converts these values into servo angles, enabling for the robotic arm to have the servos do precises movements.

One of the biggest challenges during this milestone was eliminating jittering and the unresponsive control of the servos, the code not responding, and the microcontroller shield and later the analog joysticks not response time. 

With the base project and code now complete, my future milestones will focus on improving the robotic arm's capabilities by replacing the gripper with TPU A95, replacing the various weak servos, using a worm gear to make the servos more precise and less more torque, and making the robotic arm design hopefully sleeker less dangling wires.

# Schematics 

Base Project Schematic:

<img width="630" height="667" alt="image" src="<img width="1625" height="1602" alt="Screenshot 2026-07-24 125305" src="https://github.com/user-attachments/assets/f5dbd037-8e5f-4ba4-bf9a-f48b33ea42bd" />
" />


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#include <Servo.h>

// Servo outputs
Servo baseServo;
Servo shoulderServo;
Servo elbowServo;
Servo gripperServo;

// Starting positions
int baseAngle = 90;
int shoulderAngle = 90;
int elbowAngle = 90;
int gripperAngle = 90;

// Your joysticks center around 315,
// with ends near 0 and 630.
const int LOW_LIMIT = 240;
const int HIGH_LIMIT = 390;

void setup() {
  baseServo.attach(4);       // D4
  shoulderServo.attach(5);   // D5
  elbowServo.attach(6);      // D6
  gripperServo.attach(7);    // D7

  baseServo.write(baseAngle);
  shoulderServo.write(shoulderAngle);
  elbowServo.write(elbowAngle);
  gripperServo.write(gripperAngle);

  Serial.begin(9600);
  delay(1000);
}

void loop() {
  int leftUpDown = analogRead(A0);
  int leftLeftRight = analogRead(A1);
  int rightUpDown = analogRead(A2);
  int rightLeftRight = analogRead(A3);

  // Left joystick up/down -> base servo D4
  if (leftUpDown < LOW_LIMIT) {
    baseAngle--;
  } 
  else if (leftUpDown > HIGH_LIMIT) {
    baseAngle++;
  }

  // Left joystick left/right -> shoulder servo D5
  if (leftLeftRight < LOW_LIMIT) {
    shoulderAngle--;
  } 
  else if (leftLeftRight > HIGH_LIMIT) {
    shoulderAngle++;
  }

  // Right joystick up/down -> elbow servo D6
  if (rightUpDown < LOW_LIMIT) {
    elbowAngle--;
  } 
  else if (rightUpDown > HIGH_LIMIT) {
    elbowAngle++;
  }

  // Right joystick left/right -> gripper servo D7
  if (rightLeftRight < LOW_LIMIT) {
    gripperAngle--;
  } 
  else if (rightLeftRight > HIGH_LIMIT) {
    gripperAngle++;
  }

  // Prevent servos from pushing too far
  baseAngle = constrain(baseAngle, 10, 170);
  shoulderAngle = constrain(shoulderAngle, 20, 160);
  elbowAngle = constrain(elbowAngle, 20, 160);
  gripperAngle = constrain(gripperAngle, 30, 150);

  baseServo.write(baseAngle);
  shoulderServo.write(shoulderAngle);
  elbowServo.write(elbowAngle);
  gripperServo.write(gripperAngle);

  delay(20);
}


```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| MG90S | Robotic joint servo | $8.88 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/Miuzei-Geared-Helicopter-Arduino-Project/dp/B0BWJ4RKGV?th=1)"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.


