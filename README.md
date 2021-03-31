
Cairo University, Faculty of Engineering
Computer Engineering Department
Data Structures and Algorithms

                                                    Restaurant Management
Project Requirements

___________________________________________________________________________________________________________________________________________________________________________
Data Structures and Algorithms Project Requirements

Objectives
By the end of this project, the student should be able to: - Write a complete object-oriented C++ program with Templates that performs a non-trivial task. - Use data structures to solve a real-life problem. - Understand unstructured, natural language problem description and derive an appropriate design. - Intuitively modularize a design into independent components and divide these components among team members. Introduction
Finally, the data structures TAs have decided to give up their career and start a new less tiring business, a Restaurant. Yes, it is time to farewell bits and bytes and start working with stacks of wheat packs, queues of customers' orders and loops of Swiss roll. The TAs, however, believe that they can use computer simulation to assess and enhance their service. Currently, they have ‘M’ cooks and they want to determine the service criteria -- that is, the criteria based on which an order should be serviced (i.e. prepared) earlier or later than others, to maximize average customer satisfaction. Because the TAs are currently busy running their new business, they ask you to help them, using your programming skills and knowledge of data structures, to write a simulation program that simulates the Restaurant kitchen system and calculates some statistics that measure average customer satisfaction.
Project Phase %
Phase 1 (Week 9)
35% Phase 2 (Week 14) 65%

Orders & Cooks
The restaurant has a number of available cooks that it should prepare the incoming orders.
Orders: The following information is available for each order:
- Arrival Time Stamp: When the order was made. 
- Order Type: There are 3 types of orders: VIP, Vegan orders and Normal orders. 
      ● VIP orders must be served first before vegan and normal orders. 
      ● Vegan orders are the orders that needs to be prepared by specialized cooks using all plant-based ingredients. 
      ● Normal orders are the orders that neither VIP nor vegan. - Order Size: the number of dishes for this order (in dishes). 
- Order Price: the total order price the customer should pay. 

Cooks: At startup, the system loads (from a file) information about the available cooks. For each cook, the system will load the following information:
- Cook specialization: There are 3 types: VIP cooks, vegan cooks and Normal cooks. 
        ● VIP cooks are cooks with higher cooking abilities so they are best for doing high profile orders. 
        ● Vegan cooks are cooks that tolerates making all vegetable food. 
        ● Normal cooks are the cooks that neither VIP nor vegan. 

- Break Duration: Each cook takes a break after serving n consecutive orders.
Note: The cook speed (the number of dishes it can prepare in one timestep) is the same for all cooks of the same type.

Orders Service Criteria To determine the next order to serve (if a cook is available), the following Service Criteria should be applied for all the arrived un-serviced orders at each time step: 1) 
First, Serve VIP orders by ANY available type of cooks, 
but there is a priority based on the cook’s type over the others to prepare VIP orders: 
First use VIP Cooks THEN Normal Cooks THEN Vegan Cooks. 
This means that we don’t use Normal cook unless all VIP cooks are busy, and don’t use Vegan cooks unless all other types are busy. 

2) Second, Serve Vegan orders using available Vegan cooks ONLY. If all vegan cooks are busy, wait until one is free. 

3) Third, Serve Normal orders using any type of cooks EXCEPT vegan cooks, but First use the available Normal cooks THEN VIP cooks (if all Normal are busy). 

4) If an order cannot be served at the current time step, it should wait for the next time step to be checked if it can be serviced or not. If not, it should wait again. 
Notes: If the orders of a specific type cannot be serviced in the current time step, try to service the other types (e.g. if Vegan orders cannot be serviced in the current time step, this does NOT mean not to service the Normal orders)
That is how we prioritize the service between different order types, but how will we prioritize the service between the orders of the same type?
    ● For Vegan and Normal orders, orders that arrive first should be serviced first. 
    ● For VIP orders, there is a priority equation for deciding which of the available VIP orders to serve first. VIP orders with higher priority must be serviced first. 
    ☞ You should develop a reasonable weighted priority equation depending on at least the following factors: Order Arrival Time, Order Money, and Order Size.
    There are some additional services the restaurant offers to its customers:
    ● For Normal orders ONLY, ❑ The customer can promote it to become VIP order by paying more money 
                              ❑ The customer can cancel the order as long as it is not assigned to a cook yet 
                              ❑ If a NORMAL order waits more than N timesteps from its arrival time without being assigned to a cook, 
                                 it will be automatically promoted to be a VIP order. (N is read from the input file)

Simulation Approach & Assumptions You will use incremental time steps. You will divide the time into discrete time steps of 1 unit time each and simulate the changes in the system at each timestep. 

Some Definitions 
      ● Arrival Time ( AT ): The timestep at which the order is issued by the customer.
      ● Waiting Order: The order that has arrived (i.e. Order AT < current timestep but not served yet). 
      At each time step, you should choose the orders to prepare from the waiting orders.
      ● In-service Order: The order that are being prepared (assigned to a cook) but not finished yet.
      ● Serviced Order: The order that is finished and serviced to the customer.
      ● Waiting Time ( WT ): The time interval from the arrival of an order until it is assigned to a cook.
      ● Service Time ( ST ): The time interval that a cook needs to prepare an order (the time spent in preparing the dishes).
      ● Finish Time ( FT ): The timestep at which the order is successfully serviced to the customer. FT = AT + WT + ST
      
      
      
Assumptions :
      - If the cook is available at timestep T, he/she can prepare a new order starting from that timestep. 
      - More than one order can arrive at the same timestep. 
      Also, more than one order can be assigned to different cooks at the same timestep as long as there are available cooks to prepare them. 
      - A cook can only be preparing one order at a time. - A cook cannot be assigned an order during his break.


Input/Output File Formats
    Your program should receive all information to be simulated from an input file and produces an output file that contains some information and statistics about the simulation.
    This section describes the format of both files and gives a sample for each. The Input File Format
            ● The 1st line contains three integers: N G V Each integer represents the number of cooks of different types.
            ❑ N for normal, G for vegan, and V for VIP cooks. 
            ● First 2nd line contains three integers: SN SG SV 
            ❑ SN: the speed of normal cooks ❑ SG: the speed of vegan cooks ❑ SV: the speed of VIP cooks.
            ● The 3rd line contains four integers: BO BN BG BV 
            ❑ BO: the number of orders a cook must prepare before taking a break 
            ❑ BN: the break duration (in timesteps) for normal cooks ❑ BG: the break duration for vegan ones ❑ BV: the break duration for VIP cooks. 
            ● Then a line with only one integer AutoP that represent the number of timesteps after which an order is automatically promoted to VIP.
            ● The next line contains one integer M that represents the number of events 
            ● Then the input file contains M lines (one line for each event). An event can be: 
            ❑ Arrival of a new order. Denoted by letter R, or ❑ Cancellation of an existing order. Denoted by letter X, or ❑ Promotion of an order to be a VIP order. Denoted by letter P.


NOTE: The lines of all events are sorted by the event time (TS) in ascending order.
Events Lines
• Arrival event line have the following info 
❑ R(letter R in the beginning of its line) means an arrival event ❑ TYP is the order type (N: normal, G: vegan, V: VIP). ❑ TS is the event timestep. (order arrival time) ❑ ID is a unique sequence number that identifies each order. ❑ SIZE is the number of dishes of the order ❑ MONY is the total order money.
• Cancellation event line have the following info ❑ X(Letter X) means an order cancellation event
❑ TS is the event timestep. ❑ ID is the id of the order to be canceled. This ID must be of a Normal order.

• Promotion event line have the following info ❑ P(Letter P) means an order promotion event occurring ❑ TS is the event timestep. ❑ ID is the id of the order to be promoted to be VIP. It must be of a Normal order. ❑ ExMony if the extra money the customer paid for promotion.


Sample Input File :
                    5 3 1 ➔ no. of cooks for each type 
                    2 3 6 ➔ cooks speeds for each type 
                    3 4 3 2 ➔ Breaks info line 
                    25 ➔ Auto promotion limit 
                    8 ➔ no. of events in this file 
                    R N 7 1 15 110 ➔ Arrival events example 
                    R N 9 2 7 56 
                    R V 9 3 21 300 
                    R G 12 4 53 42 
                    X 15 1 ➔ Cancellation event example 
                    R N 19 5 17 95 P 19 2 62 ➔ Promotion event example R G 25 6 33 127


The Output File Format
The output file you are required to produce should contain M output line of the format FT ID AT WT ST
which means that the order identified by sequence number ID has arrived at time AT.
It then waited for a period WT to be served. It has then taken ST ticks to be prepared and finished at timestep FT.
The output lines must be sorted by FT in ascending order. If more than one order is finished at the same timestep, they should be ordered by ST.

Then the following statistics should be shown at the end of the file 
      1- Total number of orders and total number of each order type 
      2- Total number of cooks and total number of each type 
      3- Average waiting, and average service time 
      4- Percentage of automatically-promoted orders (relative to total normal orders)
      
      
      
Sample Output File :
The following numbers are just for clarification and are not produced by actual calculations. 
                  FT ID AT WT ST 
                  18 1 7 5 6 
                  44 10 24 2 18 
                  49 4 12 20 17 
                  ………… and so on ………………… 
                  Orders: 124 [Norm:100, Veg:15, VIP:9] 
                  cooks: 9 [Norm:5, Veg:3, VIP:1] 
                  Avg Wait = 12.3, Avg Serv = 25.65 
                  Auto-promoted: 7




Program Interface The program can run in one of three modes: interactive, step-by-step or silent mode. 
When the program runs, it should ask the user to select the program mode.

Interactive mode: allows user to monitor the restaurant operation. At each time step, program should provide output similar to that in the figure.
(check document to see figure)--
In this mode, program pauses for a user mouse click to display the output of the next timestep.
At the bottom of the screen, the following information should be printed: 
    - Simulation Timestep Number 
    - Number of waiting orders of each order type 
    - Number of available cook of each type 
    - Type & ID for ALL cooks and orders that were assigned in the last timestep only. 
    e.g. N6(V3) ➔ normal cook#6 is assigned VIP order#3 to prepare 
    - Total number of orders served so far of each order type

Step-by-step mode is identical to interactive mode except that each time step, the program waits for one second (not for mouse click) then resumes automatically.
☞ You are provided a code library (set of functions) for drawing the above interface. 
(See - Appendix A) 

In silent mode, the program produces only an output file (See the “File Formats” section).
It does not draw anything graphically. No matter what mode of operation your program is running, the output file should be produced.

