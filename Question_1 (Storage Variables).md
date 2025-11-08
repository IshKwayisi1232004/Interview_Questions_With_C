## What is the a versatile variable, volatile variable and auto variable?

## * Auto Variable - when a local function is called an auto variable defined within the function is created automatically. However, when the function ends, the variable is destroyed. 
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
