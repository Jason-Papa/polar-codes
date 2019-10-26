# Polar Codes in Python

A library written in Python3 for **Polar Codes**, a capacity-achieving channel coding technique used in 5G. The library includes functions for **construction, encoding, decoding, and simulation** of polar codes. In addition, it supports **puncturing and shortening**.

It provides:
 - non-systemic encoder and Successive Cancellation Decoder (SCD) for polar codes
 - mothercode construction of polar codes using Bhattacharyya Bounds or Gaussian Approximation
 - support for puncturing and shortening
 - Bit-Reversal Shortening (BRS), Wang-Liu Shortening (WLS), and Bioglio-Gabry-Land (BGL) shortening constructions
 - an AWGN channel with BPSK modulation
 
 [![IMAGE ALT TEXT](http://img.youtube.com/vi/v47rn77RAxM/0.jpg)](http://www.youtube.com/watch?v=v47rn77RAxM "A Library for Polar Codes in Python")
 
## Getting Started

1. Download the main library package from this repository, and unzip it in "root".
2. Install matplotlib from https://matplotlib.org/users/installing.html.
3. Install numpy from https://docs.scipy.org/doc/numpy/user/install.html.
4. Run test.py using a Python3 compiler. If the program runs successfully, the library is ready to use. Make sure the compiler has writing access to directory "root/data", where simulation data will be saved by default.
5. Run main.py to start the GUI.

## Example
### Mothercode Encoding & Decoding
An example of encoding and decoding over an AWGN channel for a (256,100) mothercode, using Bhattacharyya Bounds and SCD.

```python
   import numpy as np
   from classes.PolarCode import PolarCode
   from classes.Construct import Construct
   from classes.Encode import Encode
   from classes.Decode import Decode
   from classes.AWGN import AWGN


    # initialise polar code
    myPC = PolarCode(256, 100)
    
    # mothercode construction
    design_SNR  = 5.0
    Construct(myPC, design_SNR)
    print(myPC, "\n\n")
    
    # set message
    my_message = np.random.randint(2, size=myPC.K)
    myPC.set_message(my_message)
    print("The message is:", my_message)
    
    # encode message
    Encode(myPC)
    print("The coded message is:", myPC.x)
    
    # transmit the codeword
    AWGN(myPC, design_SNR)
    print("The log-likelihoods are:", myPC.likelihoods)
    
    # decode the received codeword
    Decode(myPC)
    print("The decoded message is:", myPC.message_received)
```

### Simulation & Plotting
A script to simulate a defined polar code, save the data to a *JSON* file in directory "/data", and then display the result in a *matplotlib* figure.

```python
    # simulate polar code (default settings)
    myPC.simulate('data/brs')
    
    # plot the frame error rate
    myPC.plot(['brs'], 'data/')
```

##### This is a final year project created by Brendon McBain under the supervision of Harish Vangala at Monash University.
