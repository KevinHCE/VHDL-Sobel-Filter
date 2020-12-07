# VHDL-Sobel-Filter
A sobel filter for image processing done entirely in VHDL. Assumes the image is currently in greyscale format. This was sectioned out from a senior design project developed by Kevin Hughes, Adam Haarth, Colton Agathan, Connor Kroll, and Michael Dougherty. The original project can be located here: https://github.com/haarthad/GestureRecognition

# CAMERA_PACK.vhd
Contains constant definitions specific to the Altera D5M Camera module (used during the development of the Gesture Recognition project)

# clock_divider.vhd
Simple clock division component

# horizontal_sobel.vhd
Used to calculate the horizontal sobel output of a 3x3 pixel matrix
  Input : 3x3 8-bit pixel matrix
  Output: 10-bit horizontally based convolution value of the pixels 

# vertical_sobel.vhd
Used to calculate the vertical sobel output of a 3x3 pixel matrix
  Input : 3x3 8-bit pixel matrix
  Output: 10-bit vertically based convolution value of the pixels
  
# sobel_combination
Squares and adds the horizontal and vertical sobel convolution values
  Input : 10-bit Horizontal and vertical sobel convolution values
  Output: 21-bit edge detection magnitude squared

# lookup_table
Approximates the magnitude of edge detection at a given point, replaces performing a lengthy square root function; This was done to avoid requiring multiple clock signals to detect if an edge within an image
  Input : 21-bit edge detection magnitude squared
  Output: 7-bit edge detection magnitude approximation
  
# sobel_alu
Combination of the horizontal_sobel, vertical_sobel, sobel_combination, and lookup_table components
  Input : 3x3 8-bit pixel matrix
  Output: 7-bit edge detection magnitude approximation
  
# sobel_controller
Sample controller for the sobel ALU component
  Input : Reset signal, 50[MHz] clock, Enable signal
  Output: Sobel complete signal, Register addresses where the pixels to test would be attached to
  
# tb_sobel_alu
Testbench implementation for the sobel_alu component

# tb_sobel_controller
Testbench implementation for the sobel_controller component
