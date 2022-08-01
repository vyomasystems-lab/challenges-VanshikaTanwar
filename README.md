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
