## Getting Started

1. Download the main library package from [GitHub short URL], and unzip it in "root".
2. Install matplotlib from https://matplotlib.org/users/installing.html.
3. Install numpy from https://docs.scipy.org/doc/numpy/user/install.html.
4. Run test.py using a Python3 compiler. If the program runs successfully, the library is ready to use. Make sure the compiler has writing access to directory "root/data", where simulation data will be saved by default.

## Example
### Encoding & Decoding a Mothercode
An example of encoding and decoding over an AWGN channel for a (256,100) mothercode, using Bhattacharyya Bounds and SCD.

```python
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
    Eb_No_normalised = myPC.get_normalised_SNR(design_SNR)
    AWGN(myPC, Eb_No_normalised, 1)
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

