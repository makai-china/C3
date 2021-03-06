
     C3 version 5:   Cluster Command & Control Suite
         Oak Ridge National Laboratory, Oak Ridge, TN,
    Authors: M.Brim, R.Flanery, G.A.Geist, B.Luethke, S.L.Scott
          Thomas Naughton, Geoffroy Vallee, Wesley Bland

          Copyright (c) 2000-2011    Oak Ridge National Laboratory
                                     All rights reserved.



The Cluster Command and Control (C3) tool suite offers a command line
interface for system and user administration tasks on a cluster. 

 * For help or reporting a bug please e-mail <srt-contact@ornl.gov>.

 * For installation and configuration instructions see INSTALL.

 * For more detailed C3 documentation, see the 'doc/' directory.

 * For examples of scripts using the C3 tools and it's related libraries 
   see the 'contrib/' directory.


==


Note,  node position in the C3 configuration file ('/etc/c3.conf') is very
important!  The numbers used to refer to nodes correspond to their index in
the C3 configuration file (c3.conf), numbering is zero indexed.  C3 version
3.0 and above allows the use of node ranges on the command line.  

To use an example, take the following c3.conf file:

   cluster local {
      htorc-00:node0  #head node
      node[1-64]      #compute nodes
      exclude 60
      node[128-256]
   }

This cluster is made up of 192 nodes. The range of name "node[1-64]" is
listed as slots 0-63 in the list. the range of names "node[128-256] fill up
the slots 64-192. 

As you can see the slot a node fills in a command line range does not
necessarily coincide with it's node name. It is also a reason to explicitly
specify that a node is dead (as opposed to commenting that line out), that
way the node at slot 63 is always the machine labeled node64. 

There are two tools added to the C3 tools suite to help manage node numbers.
cname is given a name and returns its position, or slot, that it occupies.
cnum takes a range and returns what machine names are in that slot. Please
see the c3.conf(5) and c3-range(5) man pages for more details.

Version 4.0 and above allow the use of a scalable configuration. You divide
your cluster into smaller sub-clusters than execute in a parallel. For
example

   cluster part1 {
      node1
      node[1-10]
   }
   cluster part2 {
      node11
      node[11-20]
   }

is a 20 node cluster. Since C3 can easily handle up to about a 64 node
fanout on most hardware the maximum recommended size is 64 64-way clusters,
or 4096 nodes.  See c3-scale(5) for full details.
