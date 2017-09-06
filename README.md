Genau
A Processing boilerplate for AxiDraw.

This is a simple barebone class which wraps the main EiBotBoard commands in a few handy functions without much abstraction.
The main reason for this is to facilitate the start of new AxiDraw sketches.

The movement and position units are just 1/16 motor steps (Integers) where 80 steps = 1mm.
Some timing information is available (TODO).
Some boundary checking is done and 'manual reset' methods are provided as well.
A dummy port is provided to test the software without the AxiDraw connected.
A few helper functions are provided. 


The main motion methods: 
  .move(int dx, int dy)        moves the pen by [dx,dy] steps 
  .moveTo(int x, int y)        moves the pen to [x,y] (in steps), assumes a reset has been done
  .up()                        raises the pen
  .down()                      lowers the pen
  .doManualReset()             de-energises the motors to allow manual reset of the pen
  .zero()                      sets the zero, aka home
  .motorsOff()                 de-energises the motors
  
  
The main set methods:
  .setMotorSpeed(int s)        sets the motor speed (100..2000)
  .setServoDelay(int r, int l) sets the delay (in ms) before raise and after lower of the pen
  .setSevo(int d, int u)       sets the down and up value (1..65535) of the servo
  .setPosFromQuery()           reads the current step positions (QS) from the board and sets them locally


The main get methods:
  .getPos()                    returns the local positions, in steps
  .isIdle()                    returns true if the pen is not moving (works for a single command at a time)
  .isZero()                    returns true if the AxiDraw has been manually resetted (default)
  
  
The main serial queries:  
  .queryPen()
  .queryMotor()
  .querySteps()
  .version()
  
  
Helpers:  
  findSerial()                 returns a Serial object if an EBB board has been detectd, null otherwise
  messageLoop()                a crappy message sync loop "listener" to throw into Processing’s main draw() loop
  bezierLength()               'caclculates' the length of a bezier curve
  