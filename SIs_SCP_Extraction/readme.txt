
how to  write a structure of interest file:
t # 0
v 0 degree of vertex 0
v 1 degree of vertex 1
v 2 degree of vertex 2
v 3 degree of vertex 3
.
.
.
.
e 0 1     ---------------------- indicates vertex between 0 and 1 index
e 2 8     ---------------------- indicates vertex between 2 and 8 index



eg :
for a triangle each vertex has degree 2 as seen below. vertex ids are started frok 0 default and incremented by 1. 

         0
	/ \
       /   \
      /     \
      1-----2

so strucutre of interest format for traingle will be
t # 0
v 0 2
v 1 2
v 2 2
e 0 1
e 1 2
e 0 1

similiarly for a 3 path
 
0--------1
	  \
           \
	    \
	     2
so input format would be
t # 1
v 0 1 ------------since vertex 0 has only one degree ie.1 index
v 1 2 ------------ since index 1 is attached to 0 and 2 
v 2 1 ------------ since vertex index 2 is attached to only index 1
e 0 1 -------------there is a edge between index 0 and 1
e 1 2 -------------there is a edge between index 1 and 2

end with t # -1 


How to run:
python -m gspan_mining -s "minRF percentage" "GraphDataset" "structure of interest input file"

eg: python -m gspan_mining -s 0.2 ./graphdata/papertoydata.txt  si.data


output format:

file name: "Datasetname_Flatra.txt" -----> contains flat transactions
           "Datasetname"_sid_stats.txt" ----> contains SID statistics
	   "Datasetname_SIs_SIDs.txt"--------> contains SIs and corresponding subgraph ids.

The above input example outputs the all frequent graphs which are strucutre of interest and occur atleast 0.2*(size of daraset which is 10 here) times.
eg: si_2_papertoydata_results.txt and 2_papertoydata_sid_stats.txt.txt


After extracting flat transactions, run DIV_New_cmine_mapreduce.py using

python DIV_New_cmine_mapreduce.py $minRF $minCS $maxOR $minDIV $proc $1 pre $1\_$dataset\_Output.txt 2_papertoydata_Flatra.txt

Here proc defines the number of machines.

The DIV_New_cmine_mapreduce.py  need pyspark mapredue installed. 

The DIV_New_cmine_mapreduce.py takes the file "Datasetname.txt_SIs_SIDs.txt as input.

Output: 
	 DIV_New_cmine_mapreduce.py will generate the "Datasetname_Flatra.txt_output.txt" file which contains the Nscp, Np, Ts and Tscp values.
