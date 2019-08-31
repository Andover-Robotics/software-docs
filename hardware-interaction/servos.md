# Servos

Servos are rotating motors that can turn parts within a semicircular range. (For more specific information, ask a member of the build team and/or go here: https://www.servocity.com/what-is-a-servo)

To program servos, the first thing you need to do is to import the Servo class, using this command:

import com.qualcomm.robotcore.hardware.Servo;

You'll need to initialize an instance of this class within your OpMode (Servo whatever;). Inside the runOpMode method (or desired method if you're working in iterative), you can set the value of this servo to hardwareMap.servo.get(servoName);, where you would replace "servoName" with the name of the Servo on your Robot Controller.

Now that you've connected the servo you're working with to the code, you need to make a variable for the servo's numerical position. The range of numbers usefully accepted by the Servo class is 0-1, where 0 represents 0 degrees (relative) and 1 represents 180 degrees. (Of course 0.5 would be 90 degrees and so on)

To actually set the position to a variable, the Servo class has the .setPosition method. Call it using your variable as a parameter, and you've set the position!

(Tip: in order to keep it at that position for a certain amount of time without executing any other commands, use the sleep function, which takes in the number of milliseconds as a parameter and waits for that much time before going on.)




