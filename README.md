# challenges-VanshikaTanwar
challenges-VanshikaTanwar created by GitHub Classroom

# Magnitude Comparator Design Verification

The verification environment is setup using [Vyoma's UpTickPro](https://vyomasystems.com) provided for the hackathon.

![pic](https://user-images.githubusercontent.com/90523478/182223731-71e6590f-865e-47c6-aba7-f767e7dde941.jpeg)

## Verification Environment

The [CoCoTb](https://www.cocotb.org/) based Python test is developed as explained. The test drives inputs to the Design Under Test (dvsd_cmp module here) which takes in 4-bit inputs *A_in* and *B_in* and gives output accordingly. 

The values are assigned to the input port using 
```
dut.A_in.value = A_in
dut.B_in.value = B_in

```

The assert statement is used for comparing the Magnitude Comparator's output to the expected value.

The following error is seen:
```
assert dut.equal_to.value == (A_in==B_in), "Randomised test failed with: {A_in} == {B_in} = {EQUAL_TO}".format(
                     AssertionError: Randomised test failed with: 0100 == 0101 = 1
```

![image](https://user-images.githubusercontent.com/90523478/182231353-792ff220-7610-4b36-80d2-8369d8881f63.png)


![image](https://user-images.githubusercontent.com/90523478/182231389-3c5e5ed8-1b08-4d26-8068-e6c7e2d133b9.png)


## Test Scenario **(Important)**
- Test Inputs: A_in=5 B_in=10
- Expected Output: (A_in == B_in) = equal_to
- Observed Output in the DUT (dut.equal_to.value):5

Output mismatches for the above inputs proving that there is a design bug

## Design Bug
Based on the above test input and analysing the design, we see the following

```
always @(A_in or B_in)
 begin
        //This block checks if A is Greater than B, Greater than is high
       if(A_in > B_in)                              
           begin                                        
                      less_than = 4'b0;      
                      equal_to =4'b0;
                      greater_than = 4'b1;    
           end
        //This block checks if A is equal to B, Equal to is high
       else if(A_in != B_in)                                             ====> BUG
           begin                            
                      less_than = 4'b0;
                      equal_to = 4'b1;
                      greater_than = 4'b0;    
           end
        //Otherwise -This block checks for A less than B, Less than is high          
       else                                                  
           begin                                                  
                      less_than = 4'b1;
                      equal_to = 4'b0;
                      greater_than =4'b0;
        end
 end
```
For the Magnitude Comparator Design, the logic should be ``A_in == B_in`` instead of ``A_in != B_in`` as in the design code.

![image](https://user-images.githubusercontent.com/90523478/182229750-7af6bdd6-a818-41b9-a4f5-59f03876b4c9.png)


![image](https://user-images.githubusercontent.com/90523478/182229861-073bfce7-aae4-45b4-9903-e55890979e52.png)


![image](https://user-images.githubusercontent.com/90523478/182229919-fad5de1a-1fbe-4f56-9b9e-2b042b021f28.png)


## References

https://github.com/VanshikaTanwar/dvsd_4bit_magnitude_comparator.git


## Author

- [Vanshika Tanwar](https://github.com/vanishka-tanwar), Bachelor of Technology in Electronics & Communication Engineering,Dronacharya Group of Institutions,Greater Noida, U.P.
