# Binary_To_Gray_Code_Converter

  * [Abstract](#abstract)
  * [Reference Truth Table](#reference-truth-table)
  * [Modification of Equations](#minimized-equations)
  * [Kmaps](#kmaps)
  * [Formation of Minimized Circuit](#minimized-circuit)
  * [Tools Used](#tools-used)
  * [Netlist](#netlist)
  * [Ngspice Output Waveforms](#ngspice-output-waveforms)
  * [Layout](#layout)
  * [Final Layout](#final-layout)
  * [Final Output Waveform](#final-output-waveform)
  * [Conclusion](#conclusion)
  * [Author](#author)
  * [Acknowledgement](#acknowledgement)
  * [References](#references)


## Abstract
Gray Code system is a binary number system in which every successive pair of numbers differs in only one bit. It is used in applications in which the normal sequence of binary numbers generated by the hardware may produce an error or ambiguity during the transition from one number to the next.Gray code – also known as Cyclic Code, Reflected Binary Code (RBC), Reflected Binary (RB) or Grey code – is defined as an ordering of the binary number system such that each incremental value can only differ by one bit. In gray code, while traversing from one step to another step only one bit in the code group changes. That is to say that two adjacent code numbers differ from each other by only one bit.

Gray code is the most popular of the unit distance codes, but it is not suitable for arithmetic operations. Gray code has some applications in analog to digital converters, as well as being used for error correction in digital communication.

## Reference Truth Table

![IMG_20220405_155250](https://user-images.githubusercontent.com/59500283/161821480-1f06e8c3-1ecf-4aae-b8e9-f5c283aded76.jpg)


## Minimized Equations

![IMG_20220405_162058](https://user-images.githubusercontent.com/59500283/161821592-86df7a61-3f95-4efa-8b93-4131234bca7f.jpg)

![IMG_20220405_162148](https://user-images.githubusercontent.com/59500283/161821638-50d19ca7-05ff-4fae-90f6-82c13ff68fe6.jpg)

## Kmaps

![KMAP](https://user-images.githubusercontent.com/59500283/161933708-727277d5-439f-4199-8556-633960ff3058.jpg)


![KMAP_1](https://user-images.githubusercontent.com/59500283/161933620-6cfbe1d0-9659-476f-ac68-d1cdc02eac47.jpg)



## Minimized Circuit 

![IMG_20220405_152809](https://user-images.githubusercontent.com/59500283/161822051-b5780ba1-e1e2-468b-817b-4463560a1b33.jpg)


## Tools Used:

![NGSPICE](https://user-images.githubusercontent.com/59500283/161823202-f5325839-fe04-4437-842a-f9432029402c.jpeg)
![Microwind](https://user-images.githubusercontent.com/59500283/161823254-2cd4a00b-dc74-4414-9fdf-7bda42d83534.jpeg)


## Simulation in NGSPICE

Formation of Netlist For the Required Circuits.

Step-1 : Numbering the Elements According to the rules.

![IMG_20220405_164759](https://user-images.githubusercontent.com/59500283/161823729-73c7d250-7a6d-4515-a705-51c0529aff2b.jpg)


Step-2 : Recognize the Sub-Circuits and Numbering them.

![IMG_20220405_165339](https://user-images.githubusercontent.com/59500283/161823787-3868b128-9a02-4584-a8a3-b5908d8751b4.jpg)

Step-3 : Writing the Netlist for each Sub-Circuit and merging them according to the Circuit.

## Netlist

**Binary To Grey Code Conversion

.subckt inverter 1 2 3

mp 2 1 3 3 pmod w=100u l=1u

mn 2 1 0 0 nmod w=40u l=1u

.model pmod pmos Vto=-1V Kp=80u

.model nmod nmos Vto=1V Kp=200u

.ends

.subckt pass_and 1 2 3 4

m1 1 2 4 4 nmod w=40u l=1u

m2 2 3 4 4 nmod w=40u l=1u

.model nmod nmos Vto=1 Kp=200u

.ends

.subckt pass_xor 1 2 3 4 5

m1 1 4 5 5 nmod w=40u l=1u

m2 3 2 5 5 nmod w=40u l=1u

.model nmod nmos Vto=1V Kp=200u

.ends

Vdd 1 0 dc 5V

Va 10 0 pulse(0 5 0 0 0 16ns 32ns)

Vb 11 0 dc 5V

Vc 12 0 dc 5V

Vd 13 0 dc 5V

xa 10 14 1 inverter

xb 11 15 1 inverter

xc 12 16 1 inverter

xd 13 17 1 inverter

xa_xor_b 10 11 14 15 18 pass_xor

xb_xor_c 11 12 15 16 19 pass_xor

xc_xor_d 12 13 16 17 20 pass_xor

xd_and_d 13 13 17 21 pass_and

.tran 0.1ns 32ns

.control

run

plot V(10) 

plot V(11) 

plot V(12) 

plot V(13) 

plot V(18)

plot V(19)

plot V(20)

plot V(21)

.endc 

.end


## Ngspice Output Waveforms

# B0

<img width="802" alt="B0" src="https://user-images.githubusercontent.com/59500283/161847825-c5ec3078-5b55-40ec-92a4-a391b9f84e16.png">


# B1

<img width="683" alt="B1" src="https://user-images.githubusercontent.com/59500283/161847869-d0fbc1b7-0ab1-468e-b707-848694b0a7dd.png">


# B2

<img width="683" alt="B2" src="https://user-images.githubusercontent.com/59500283/161847903-dcc183ce-6838-4b0b-9481-de70dc7088bc.png">


# B3


<img width="652" alt="B3" src="https://user-images.githubusercontent.com/59500283/161847966-51909b37-06f8-48e3-8c27-de549dc8329f.png">


# G0


<img width="674" alt="G0" src="https://user-images.githubusercontent.com/59500283/161848117-953d1024-1055-474a-90e6-7cf53daf9be6.png">



# G1


<img width="672" alt="G1" src="https://user-images.githubusercontent.com/59500283/161848144-57c48ff6-86ef-4a29-b7ba-3cbfa33301cb.png">


# G2


<img width="668" alt="G2" src="https://user-images.githubusercontent.com/59500283/161848164-4e5e22ef-58bb-40de-8bdc-5d255cde6056.png">


# G3


<img width="641" alt="G3" src="https://user-images.githubusercontent.com/59500283/161848187-d8572353-11c1-46d9-9f0f-d85e11ba5cc2.png">



## Layout

Step-1:Make the Layouts of Small Circuits Which we require .
Circuits Required-

# Inverter (For Inverted Input)

<img width="625" alt="Inverter" src="https://user-images.githubusercontent.com/59500283/161848981-8081be88-ba89-4cb2-98ae-46b319b34106.png">

# Inverter Output Waveform

<img width="1438" alt="Inverter_Waveform" src="https://user-images.githubusercontent.com/59500283/161849051-0ad8dd3a-1981-4fbb-b99a-b1007e5e9339.png">

# Xor Gate

<img width="717" alt="Xor_Layout" src="https://user-images.githubusercontent.com/59500283/161849097-844caa1f-50bf-4d39-bd44-f8614a27614f.png">


# XOR Output Waveform

<img width="1438" alt="Xor_Waveform" src="https://user-images.githubusercontent.com/59500283/161849174-1430971b-a184-40d3-8a78-68c6949ca041.png">

Step-2:Now just make multiple copies of it as per requirenment and make the connections accordingly.

# Final Layout

<img width="411" alt="Final_Layout" src="https://user-images.githubusercontent.com/59500283/161849324-a99c5a5c-732b-4969-8b20-6e27919486b9.png">

# Final Output Waveform

<img width="1440" alt="Final_Layout_Waveform" src="https://user-images.githubusercontent.com/59500283/161849371-883714f1-f41e-45d2-b71d-7f5cacd035e7.png">


## Conclusion
Thus , The Netlist and the Layout of Binary to Grey Code Converter is Achieved.

## Author
Mayur Dongre , Indian Institute of Information Technoology Nagpur.

## Acknowledgement
Dr Paritosh D. Peshwe (IIIT Nagpur)

## References
Modern Digital Electronics by RK Jain


  
