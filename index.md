Omnidirectional Robot
This project I built a robotic car, which can drive in every direction without turning. By using wheels with other wheels intagrated on to it, the robot can go backwards, forwards, left, right, and diagonally instantly with no complicated turning or manuvering. This makes the robot much more mobile and manuverable.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Callum A | University High School | Electrical Engineering | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

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

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


The project is a robotic car that can move in any direction. It can be controlled by bluetooth and linked up to an app on your phone. The base of the project is very simple, everything comes in a kit, and it has very clear instructions online. The first base project only took a few hours to build and modify to be bluetooth capable. I planned to, and built it by folowing the online schematics and code provided for me. Since the code and electronics schemitics were provided for me the first milestone posed very few difficulties. My plan moving foreward is to connect the robot to my ps4 controller instead of the app made by the company on my phone. This would make it so I have to re-write the code and figure out how to implement it with my ps4 controller. I think some challenges will be re-writing the code and making it work with the ps4 controller.
For your first milestone, describe what your project is and how you plan to build it. You can include:


# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
#define MAX_PACKETSIZE 32    //Serial receive buffer
char buffUART[MAX_PACKETSIZE];
unsigned int buffUARTIndex = 0;
unsigned long preUARTTick = 0;
struct car_status{
  int speed;
  int angle;
  int direct;
};
int move_speed=100 ;

#define MAX_SPEED  250
#define MIN_SPEED  50

#define TURN_SPEED  70
#define SLOW_TURN_SPEED  50
#define BACK_SPEED  60

int buttonState;
char old_status='0';
#define speedPinR 9   //  Front Wheel PWM pin connect Model-Y M_B ENA 
#define RightMotorDirPin1  22    //Front Right Motor direction pin 1 to Model-Y M_B IN1  (K1)
#define RightMotorDirPin2  24   //Front Right Motor direction pin 2 to Model-Y M_B IN2   (K1)                                 
#define LeftMotorDirPin1  26    //Front Left Motor direction pin 1 to Model-Y M_B IN3 (K3)
#define LeftMotorDirPin2  28   //Front Left Motor direction pin 2 to Model-Y M_B IN4 (K3)
#define speedPinL 10   //  Front Wheel PWM pin connect Model-Y M_B ENB

#define speedPinRB 11   //  Rear Wheel PWM pin connect Left Model-Y M_A ENA 
#define RightMotorDirPin1B  5    //Rear Right Motor direction pin 1 to Model-Y M_A IN1 ( K1)
#define RightMotorDirPin2B 6    //Rear Right Motor direction pin 2 to Model-Y M_A IN2 ( K1) 
#define LeftMotorDirPin1B 7    //Rear Left Motor direction pin 1 to Model-Y M_A IN3  (K3)
#define LeftMotorDirPin2B 8  //Rear Left Motor direction pin 2 to Model-Y M_A IN4 (K3)
#define speedPinLB 12    //  Rear Wheel PWM pin connect Model-Y M_A ENB

int car_direction = 1; // 1 means forward, 0 gear backward

/*motor control*/
void right_shift(int speed_fl_fwd,int speed_rl_bck ,int speed_rr_fwd,int speed_fr_bck) {
  FL_fwd(speed_fl_fwd); 
  RL_bck(speed_rl_bck); 
  RR_fwd(speed_rr_fwd);
  FR_bck(speed_fr_bck);
}
void left_shift(int speed_fl_bck,int speed_rl_fwd ,int speed_rr_bck,int speed_fr_fwd){
   FL_bck(speed_fl_bck);
   RL_fwd(speed_rl_fwd);
   RR_bck(speed_rr_bck);
   FR_fwd(speed_fr_fwd);
}
void go_advance(int left_speed,int right_speed){
   RL_fwd(left_speed);
   RR_fwd(right_speed);
   FR_fwd(right_speed);
   FL_fwd(left_speed); 
}
void go_back(int left_speed,int right_speed){
   RL_bck(left_speed);
   RR_bck(right_speed);
   FR_bck(right_speed);
   FL_bck(left_speed); 
}
void left_turn(int speed){
   RL_bck(speed);
   RR_fwd(speed);
   FR_fwd(speed);
   FL_bck(speed); 
}
void right_turn(int speed){
   RL_fwd(speed);
   RR_bck(speed);
   FR_bck(speed);
   FL_fwd(speed); 
}
void left_back(int speed){
   RL_fwd(0);
   RR_bck(speed);
   FR_bck(speed);
   FL_fwd(0); 
}
void right_back(int speed){
   RL_bck(speed);
   RR_fwd(0);
   FR_fwd(0);
   FL_bck(speed); 
}
void clockwise(int speed){
   RL_fwd(speed);
   RR_bck(speed);
   FR_bck(speed);
   FL_fwd(speed); 
}
void countclockwise(int speed){
   RL_bck(speed);
   RR_fwd(speed);
   FR_fwd(speed);
   FL_bck(speed); 
}
void FR_fwd(int speed)  //front-right wheel forward turn
{
  digitalWrite(RightMotorDirPin1,HIGH);
  digitalWrite(RightMotorDirPin2,LOW); 
  analogWrite(speedPinR,speed);
}
void FR_bck(int speed) // front-right wheel backward turn
{
  digitalWrite(RightMotorDirPin1,LOW);
  digitalWrite(RightMotorDirPin2,HIGH); 
  analogWrite(speedPinR,speed);
}
void FL_fwd(int speed) // front-left wheel forward turn
{
  digitalWrite(LeftMotorDirPin1,HIGH);
  digitalWrite(LeftMotorDirPin2,LOW);
  analogWrite(speedPinL,speed);
}
void FL_bck(int speed) // front-left wheel backward turn
{
  digitalWrite(LeftMotorDirPin1,LOW);
  digitalWrite(LeftMotorDirPin2,HIGH);
  analogWrite(speedPinL,speed);
}

void RR_fwd(int speed)  //rear-right wheel forward turn
{
  digitalWrite(RightMotorDirPin1B, HIGH);
  digitalWrite(RightMotorDirPin2B,LOW); 
  analogWrite(speedPinRB,speed);
}
void RR_bck(int speed)  //rear-right wheel backward turn
{
  digitalWrite(RightMotorDirPin1B, LOW);
  digitalWrite(RightMotorDirPin2B,HIGH); 
  analogWrite(speedPinRB,speed);
}
void RL_fwd(int speed)  //rear-left wheel forward turn
{
  digitalWrite(LeftMotorDirPin1B,HIGH);
  digitalWrite(LeftMotorDirPin2B,LOW);
  analogWrite(speedPinLB,speed);
}
void RL_bck(int speed)    //rear-left wheel backward turn
{
  digitalWrite(LeftMotorDirPin1B,LOW);
  digitalWrite(LeftMotorDirPin2B,HIGH);
  analogWrite(speedPinLB,speed);
}
 
 
void stop_stop()    //Stop
{
    analogWrite(speedPinLB,0);
 analogWrite(speedPinRB,0);
    analogWrite(speedPinL,0);
 analogWrite(speedPinR,0);
}


//Pins initialize
void init_GPIO()
{
  pinMode(RightMotorDirPin1, OUTPUT); 
  pinMode(RightMotorDirPin2, OUTPUT); 
  pinMode(speedPinL, OUTPUT);  
 
  pinMode(LeftMotorDirPin1, OUTPUT);
  pinMode(LeftMotorDirPin2, OUTPUT); 
  pinMode(speedPinR, OUTPUT);
     pinMode(RightMotorDirPin1B, OUTPUT); 
  pinMode(RightMotorDirPin2B, OUTPUT); 
  pinMode(speedPinLB, OUTPUT);  
 
  pinMode(LeftMotorDirPin1B, OUTPUT);
  pinMode(LeftMotorDirPin2B, OUTPUT); 
  pinMode(speedPinRB, OUTPUT);

}

void setup()
{
  init_GPIO();
    Serial.begin(9600);//In order to fit the Bluetooth module's default baud rate, only 9600
   Serial1.begin(9600);
 
 
  stop_stop();
 
}

void loop(){
 do_Uart_Tick();
}

void do_Uart_Tick()
{

  char Uart_Date=0;
  if(Serial1.available()) 
  {
    size_t len = Serial1.available();
    uint8_t sbuf[len + 1];
    sbuf[len] = 0x00;
    Serial1.readBytes(sbuf, len);
    //parseUartPackage((char*)sbuf);
    memcpy(buffUART + buffUARTIndex, sbuf, len);//ensure that the serial port can read the entire frame of data
    buffUARTIndex += len;
    preUARTTick = millis();
    if(buffUARTIndex >= MAX_PACKETSIZE - 1) 
    {
      buffUARTIndex = MAX_PACKETSIZE - 2;
      preUARTTick = preUARTTick - 200;
    }
  }
  car_status cs;
  if(buffUARTIndex > 0 && (millis() - preUARTTick >= 100))//APP send flag to modify the obstacle avoidance parameters
  { //data ready
    buffUART[buffUARTIndex] = 0x00;
    Uart_Date=buffUART[0];
    cs=get_status(buffUART);
    car_direction=cs.angle;
    buffUARTIndex = 0;
  }
  move_speed=cs.speed;
   if (cs.speed>MAX_SPEED) move_speed= MAX_SPEED;
   if (cs.speed<MIN_SPEED) move_speed= MIN_SPEED;

  switch (Uart_Date)    //serial control instructions
  {
    case 'M':  
    if(old_status=='0')
    go_advance(110,110);
    old_status='M';
    delay(35);
    go_advance(move_speed,move_speed);
    break;
    
    case 'L':  
    car_direction=1;
    if (cs.angle<2)
     go_advance(SLOW_TURN_SPEED,TURN_SPEED);
    else  left_turn(SLOW_TURN_SPEED);
    old_status='0';
    break;
    case 'R': 
      car_direction=1;
     if (cs.angle>-2)
      go_advance(TURN_SPEED,SLOW_TURN_SPEED);
     else right_turn(SLOW_TURN_SPEED); 
     old_status='0';
    break;
    case 'B':  
      car_direction=0;
    go_back(BACK_SPEED,BACK_SPEED); 
     old_status='0';
    break;
    case 'X': 
      car_direction=0;
    if (cs.angle>-2)
      go_back(SLOW_TURN_SPEED,TURN_SPEED); 
    else
      left_back(TURN_SPEED);
   old_status='0';
    break;
    case 'Y':  
     car_direction=0;
    if (cs.angle<2)
      go_back(TURN_SPEED,SLOW_TURN_SPEED); 
    else
     right_back(TURN_SPEED); 
    old_status='0';
    break;
     case 'F':  
   //   left_shift(200,150,150,200); //left shift
      left_shift(180,170,190,190) ;//left shift
      delay(800);
      old_status='0';
      break;
    case 'J':       
    //  right_shift(200,150,150,200); //right shift
         right_shift(200,170,170,200); //right shift
      delay(800);
      old_status='0';
      break;
    case 'G': 
       if (car_direction==0) left_shift(0,150,0,150); //left ahead
        else left_shift(150,0,150,0); //left back
    delay(800);
    old_status='0';
    break;
    case 'I': 
     if (car_direction==0) right_shift(180,0,150,0); //right ahead
      else  right_shift(0,130,0,130); //right back
     delay(100);
     old_status='0';
    break;
    case 'E': stop_stop(); 
         old_status='0';
    break;
    case 'H': stop_stop(); 
         old_status='0';
    break;
    default:break;
  }
}

car_status get_status( char buffUART[])
{
  car_status cstatus;
  int index=2;
  if (buffUART[index]=='-'){
    cstatus.angle=-buffUART[index+1]+'0';
    index=index+3;
    
  } else {
   
    cstatus.angle=buffUART[index]-'0';
     index=index+2;
  }
  int currentvalue;
  int spd=0;
  while (buffUART[index]!=',')
  {
    currentvalue=buffUART[index]-'0';
    spd=spd*10+currentvalue;
    index++;
  }
  cstatus.speed=spd;
  index++;
  cstatus.direct=buffUART[index]-'0';
  return cstatus;
}

```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Battery Pack | Holds batteries | $1.80 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

| AA Batteries | Power source | $9.73 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Car Chassis | Solid base of the car | $7.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Omnidirection Wheels | Wheels that allow 360 degree movement | $19.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Gear Motor | Turns the wheels | $5.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| LED Light | Placed at the front of the car for better sensor vision | $8.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Osoyoo Wi-Fi Shield | Allows car to connect to the internet and bluetooth | $12.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Mega2560 Arduino Board | Programmable circuit boared that tells wheels how to move | $20.69 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Osyoo Model Y 2.0 Motor Driver Module | Connects the motors to the other systems in the car | $19.98 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Voltage Meter | Tracks voltage running through the car| $6.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| SG 90 Servo Motor | Rotates the ultrasonic sensor to detect objects | $7.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Ultrasonic Sensor Holder + Ultrasonic Sensor | Holds ultrasonic sensor + senses the ultrasonic energy waves | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |



# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
