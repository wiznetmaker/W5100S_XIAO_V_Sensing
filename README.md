# W5100S_XIAO_V_Sensing


I don't have an oscilloscope at home. I wanted to have the smallest oscilloscope that I can use on a web page!

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/ab093d49-b11b-403c-bbba-621841715668)

## COMPONENTS
### PROJECT DESCRIPTION
#### Summary
I don't have an oscilloscope at home. I wanted to have the smallest oscilloscope that I can use on a web page! So, I tried making one using Seeed Studio's XIAO-RP2040, which is based on RP2040.

#### Hardware
![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/e4a5e75d-c698-4dff-9ac8-7ccbe1425622)

Ultra Small Ethernet + RP2040 Board Production Record

I recently developed a module that combines the XIAO-RP2040 and the Ethernet chip, W5100S.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/bef07ee5-b98f-4d55-9600-395e6e4e5cae)

The hardware configuration is as follows: a simple method of using ADC to transmit data over Ethernet.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/0f731654-abad-4915-b847-2a8332915ab4)

By simply connecting two resistors and a probe to P26, the setup is complete.
I was a little confused in the resistance calculation.

I want to measure the voltage to the second decimal place.

The Raspberry Pi RP2040 ADC has a resolution of 12 bits. In other words, the value of 0 to 3.3 V can be expressed by dividing it by 4096. I wanted to measure the voltage by 0.01V. < 0.01V * 4096 = 40.96V >. This means that if measured up to about 40V, it can be read in units of 0.01V.

3.3V is the MAX value, so the resistance value is 40B/(A + B) = 3.3.

3.3A = 36.7B

That is, it can be set at the ratio of <A:B = 36.7:3.3>. I designed with 36k : 3.3k.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/6b71ee11-2d87-4792-9259-14178f7bb698)

It was fixed with silicone so that the resistance would not fall.

#### Firmware
![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/432ef5c6-8111-4d55-9c1a-d7ad45dd996b)

It was possible to develop it comfortably using WIZnet's RP2040-only Git.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/f64e5ab0-6684-411e-af1d-169cb75154a8)

Change the pins in the corresponding code.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/571282bf-9cff-4675-aa43-df73dc6d6aad)

Since it will display a value in HTTP, it is necessary to create an HTML code.

The x-axis is set to time. The y-axis is an analog value and is set to a maximum of 40.I received the data in real time and distributed it. Please check my collar for a detailed code.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/0634166e-6a79-4f7d-ab98-7ada922a799b)

And I calculated the response value and made it. Value to be displayed on the actual web.

The ADC on the RP2040 has a resolution of 12 bits, but the representation is changed to 16 bits. In other words, the value read by adc must be divided by 65535 and multiplied by 3.3V to output the actual input. And the exact resistance I put on is 36k + 3.3k = 39.3k. Therefore, the actual voltage value that can be expressed is 39.3V instead of 40V.

39.3 / 3.3 = 11.90909

So multiply the above by 11.91. Then, when the 3.3V input comes in, the calculated value of 39.3V is output.

(0.2V is the Offset value.)


#### Test
![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/634b20b0-3553-4d7a-a51d-a3b40824156f)

Now it's time to test. Enter power to Power Supply. Unfortunately, the supply I have can only output up to 31.5V.

https://youtu.be/G7Kt-2-oFAY

Here's the motion video!

It works very smoothly and well. The ADC on the RP2040 can be read up to 500 kHz. I haven't experimented with it, but this device probably won't read at 500kHz due to multiple delays, but it will read at a rate comparable to that.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/6ccbe28d-1c1e-4d20-bc17-ce7553947932)

You'll be able to check various boards like this. The power line is so annoying that I'm going to make a PoE module next time.

![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/27a7551f-ae2b-4e41-bd7e-7591ef0ba2ad)

The design is already in its final stages. It looks a little big, but it will be made much smaller than you think.
 
![image](https://github.com/wiznetmaker/W5100S_XIAO_V_Sensing/assets/111826791/b543c51e-5c3d-4260-8f42-edb9b05bafb3)

When the board is finished, you'll be able to do anything very compact like this.

In a very, very small form!

End
There are many scopes, but there will be no such small and efficient scope! Make it very, very simple! It's so comfortable!

Additionally, there is a Raspberry Pico version. Only the pin map is a little different, and it looks better with PoE.

In addition, current detection has been added.

https://maker.wiznet.io/Alan/projects/the-worlds-smallest-oscilloscope/
