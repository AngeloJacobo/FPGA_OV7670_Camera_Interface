Created by: Angelo Jacobo   
Date: August 16,2021   

[![image](https://user-images.githubusercontent.com/87559347/129681334-1939fffe-306e-4f97-b189-46efec2e8437.png)](https://youtu.be/YJ7wrXs70nQ)


# Inside the src folder are:   
* top_module.v -> Combines the camera_interface, sdram_interface, and vga_interface modules.   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; key[1:0] for brightness control   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; key[3:2] for contrast control   
* camera_interface.v -> Configures the register of OV7670 via SCCB protocol. Pixel data is  also retrieved from    
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;the camera and then passed to asyn_fifo module   
* sdram_interface.v -> Controls the logic sequence for storing the pixel data retrieved from the camera_interface  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; module and then sending it to the asyn_fifo connected to vga_interface module   
* vga_interface.v -> Passes the pixel data retrieved from sdram to the vga_core module   
* asyn_fifo.v -> FIFO with separate clock domains for read and write. Solves the clock domain crossing issue(see  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; image below)        
* i2c_top.v -> Bit-bang implementation of SCCB(which is very similar to i2c)     
* sdram_controller.v -> Controller for storing to and retrieving data from SDRAM. Optimized to a memory     
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; bandwidth of 316MB/s     
* vga_core.v -> VGA controller. Set at 640x480 @ 60fps     
* top_module.ucf -> Constraint file for top_module.v       
#### **NOTE: dcm_24MHz.v , dcm_25MHz.v , and dcm_165MHz.v are PLL instantiations specific to Xilinx. Replace these files(and also the instantiation of these PLLs on the source code) when implementing this design to other FPGAs.**    

# Logic Flow:
![Camera_Interface](https://user-images.githubusercontent.com/87559347/129671784-1be86eca-7cfa-4566-9a94-96a9e9015aa7.jpg)

# About:  
This project implements a real-time streaming of OV7670 camera via VGA. The OV7670 is a 0.3 Megapixel camera(640x480) with 30 fps.
Data pixels are stored to and retrieved from SDRAM with burst mode set to "full page"(512 words).

# Donate   
Support these open-source projects by donating  

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/donate?hosted_button_id=GBJQGJNCJZVRU)


# Inquiries  
Connect with me at my linkedin: https://www.linkedin.com/in/angelo-jacobo/
