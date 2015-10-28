performance-test-using-PAPI 
=========================================
collect and calculate several performance parameters using PAPI (http://icl.cs.utk.edu/papi/) 

### parameters
* CPI =  Total_Cycles /  Total_Instructions_Exec = PAPI_TOT_CYC / PAPI_TOT_INS
* L1 cache miss rate  = L1_Misses / (Loads  + Stores) = PAPI_L1_TCM / PAPI_LST_INS
* L2 cache miss rate  = L2_Misses / L1_Misses = PAPI_L2_TCM / PAPI_L1_TCM
* TLB miss rate = TLB_Misses / (Loads + Stores) = (PAPI_TLB_DM  + PAPI_TLB_IM) / PAPI_LST_INS
* Branch miss prediction rate  = Mispredicted_Branches  / Total Branches Decoded = PAPI_BR_MSP / PAPI_BR_CN

### download and extract
        $ tar -xzvf papi-5.4.1.tar.gz
		
### modify path
        $ cd papi-5.4.1/src
        $ vim Makefile
        modify PREFIX = {path}
### install
        $ ./configure
        $ make
        $ make install
### list all supported events
        $ cd src/ctests
        $ ./all_events
### test
        $ icc papi-prime.c  -I papi/include/ papi/lib/libpapi.a  -o  papi-prime
        $ ./papi-prime
        $ icc prime2.c  -I papi/include/ papi/lib/libpapi.a  -o prime2 
        $ ./prime2
### result
* Hardware Counters     : 11
* CPI                   : 0.7444
* L1 miss rate          : 0.1846
* L2 miss rate          : 0.9864
* Hardware Counters     : 11
* TLB miss rate         : 0.0003
* BR miss predict rate  : 0.0074
        
				
