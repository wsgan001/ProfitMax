# ProfitMax version 1.1
This project is used to demonstrate the experiments for the paper: Jing Tang, Xueyan Tang, Junsong Yuan, "[Profit Maximization for Viral Marketing in Online Social Networks,](http://ieeexplore.ieee.org/document/7784445/)" in Proc. IEEE ICNP 2016.

**Author: Jing Tang (Nanyang Technological University)**
> Cross-platform supported, including **\*nix** and **Windows** systems!\
Under **\*nix** system, compile and build codes:\
`g++ -std=c++14 -O3 ProfitMax.cpp alg.cpp SFMT/dSFMT/dSFMT.c -o ProfitMax1.1.o`\
Note: `c++1x` is required.

**_Before running influence maximization algorithms, please format the graph first!_**

Execute the command: `{your_exec} [options]`. `{your_exec}` may be `ProfitMax1.1.o` under **\*nix** or `ProfitMax1.1.exe` under **Windows**.

See some sample codes in **sample-code.sh** or **sample-code.bat**. For example,

- Format the graph: 

	`{your_exec} -func=0 -gname=facebook`

- Run double greedy algorithm with iterative pruning approach:

	`{your_exec} -func=1 -gname=facebook -alg=doublegreedy -ptype=1`

- Run simple greedy algorithm without iterative pruning approach:

	`{your_exec} -func=1 -gname=facebook -alg=greedy -ptype=0`

### Options
- **-func=integer**

	Specify the function to execute. Possible values:
	+ **0**: Format the graph.
	+ **1** *[default]*: Run profit maximization algorithms.
	+ **2**: Format the graph and run profit maximization algorithms.
	
- **-dir=string**

	Specify the direction for the input files, e.g., **-dir=graphInfo** *[default]*.
    
- **-gname=string**
	
	Specify the graph name to process, e.g., **-gname=facebook** *[default]*.
    
- **-mode=string** *(works only when -func=0 or -func=2)*
	
    Specify how to format the graph file with three letters. Two types of original graph file are supported. The file should have *m+1* lines where the first line has two integers to indicate the number *n* of nodes and the number *m* of edges. The following *m* lines list the edges. The node is indexed from *0* to *n-1*. Each edge line has two integers to indicate the source node and target node.
	+ **-mode=egr** *[default]*: Weighted Cascade (WC) model is used where *p(u,v)=1/indeg(v)*. For example,
    	> 3 4\
    	0 1\
    	0 2\
    	1 0\
    	1 2
    
   + **-mode=ewr**: Each edge line can also follow with a positive number to indicate the edge weight (probability). In this case, the probability weight is associated by the given value. For example,
    	> 3 4\
    	0 1 0.2\
    	0 2 0.3\
    	1 0 0.1\
    	1 2 0.4

	The following options are valid for *-func=1* or *-func=2*.

- **-outpath=string**
	
    Specify the folder to save results, e.g., **-outpath=result** *[default]*.
- **-alg=string**
	
    Specify the algorithm used for profit maximization. Possible values:
	+ **random**: Random algorithm.
	+ **highdegree**: High-Degree algorithm.
	+ **infmax**: Influence maximization algorithms such as IMM and BCT.
	+ **greedy**: Simple greedy algorithm.
	+ **doublegreedy** *[default]*: Double greedy algorithm.
	
- **-model=string**
	
    Specify the cascade model. Possible values:
	+ **IC** *[default]*: Independent Cascade model.
	+ **LT**: Linear Threshold cascade model.
	
- **-scale=decimal**
	
    Specify the ratio between the total cost and total benefit of all the nodes. The default value is *10.0*.
    
- **-para=decimal**
	
    Specify the fraction of base cost for each node. Allowed value is *0* to *1*. When this parameter is set to *0* *[default]*, the seed selection cost of each node is completely proportional to its social degree. When this parameter is set to *1*, the seed selection cost of each node is the same (uniform).
    
- **-numR=integer**
	
    Specify the number of RR sets generated for the greedy algorithms. The default value is *1,000,000*.
    
-  **-ptype=boolean**

	Specify the graph name to process. Possible values:
	+ **0** *[default]*: Iterative pruning approach is NOT used.
	+ **1**: Iterative pruning approach is used.
