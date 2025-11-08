## What is the a versatile variable, volatile variable and auto variable?

## Auto Variable - when a local function is called an auto variable defined within the function is created automatically. However, when the function ends, the variable is destroyed. 
  - Here is an example in code: 

        void test() {
          auto int x = 10;  // 'auto' is optional
          printf("%d", x);
        }
    
  - In this example, x is being called into the stack, but only exists within the function variable (i.e. this is a private variable). Once the last line of the function is 
    complete, variable "x" is deleted from the stack.
  - The main reason why we use an auto variable is because its temporary, fast, and private for sitautions where we want:
    * Efficient stack allocation 
    * Has no affect on code outside the function
    * Need for short operations
  - For example, in a scenario where we are reading a sensor value:
    * An auto variable is needed because: 
      > The variables are only needed inside this function (no where else in the program) 
      > Memory stack they used is automatically deleted, keeping it safe and efficient 
    * Why not use another storage type?
      > If you used a static variable, it would persist forever... causing inefficient memory.
      > If you used a gloabl variable, it could be changed anywhere outside the function -> dangerous.
      
## Volatile Variable - tells the compiler the value of this variable can change any time. Influences outside of the code, can directly change the variable.
  - Influences outside of the code can come in the form of:
    * Hardware
    * Interrupts
    * Other threads (in RTOS or multi-core systems)
  - Embedded System Use Case
    * Imagine you want your hardware register to change based on sensor updates.

          volatile int sensor_data;

          void loop() {
              while (sensor_data == 0) {
                  // wait for new sensor data
                  // without volatile, compiler might optimize this loop away
              }
              printf("New data: %d\n", sensor_data);
          }

    * The volatile variable within the code tells the compiler that sensor_data can change. Ensuring that the it sees the latest hardware value.
    * Providing accurate behavior when external hardware changes the variable values.
    * This is used for:
      > Hardware registers
      
      > Interrupt flags
      
      > Shared memory
  
## Register Variable - tells the compiler the variable will be used frequently. Informing that the variable should be stored in a CPU register, rather than RAM. Allowing for faster access for the variable. 
  - However, it should be noted that modern compilers ignore this because they are more reliable and effiecient in managing registers in comparison to hunmans.
  - This is used in embedded systems for tight loops or ISR routines
  - 
