Structured Data
	Easy to compare numerically.
	Use computer to perform mathematical operations

Unstructured Data
	Difficult to understand
	Difficult to quantify as numbers
	
	Image
	Audio
	Video
	Text

How do computers translate unstructured data?

How do we make sure meaning doesn't get lost in this translation from human to machine language?

Human-Understandable Data

	Text
		Read words one after the another
	Image [Stacked pixels]
		As Objects interacting with each another
	Audio [Sound intensity and frequencies]
		Listen and Understanable
	Video
		Time evolution of images [Played forwarded]

Computer
	Image
		Milllions of Pixels stacked on each other [Each Pixel has number associated]
		Trail of numbers -- visual features (can be represented as number)
	Text
		Convert into millions of words.
		Co-occurence of words.

	Audio/Video
		Can be represented as numbers, summarised as smaller groups of numbers, [content, pattern, concepts]

	Group of numbers as known as Vector
	Vector captures meaning behind the data.

	No meaning is lost while translating from Human readable to computer/Machine readable.

Visualize vector representation of data.
	Color	-- RGB [3D Vector]
	Magenta   (255,0,255) 
	Violet	  (127,0,255)
	Turquoise (64,224,208)	

Vector Drawn out 
	Direction and Magnitude/Length

	Based upon Direction and Length ,Vector can differentiate between similarities and differences


Similar and Dissimilar datapoints
	
	Euclidean Distance (L2)
		d = √[ (x2 – x1)2 + (y2 – y1)2] (extend it to N-D)
		Shortest Distnace between 2 vectors
	Manhattan Distance (L1)
		d = [ (x2 – x1) + (y2 – y1)] (extend it to N-D)
		If we move along the dimensions of the data.
	Cosine Distance
		1- (A*B/||A||||B||)
		How similar the direction of Vectors
	Dot Product
		A*B =Sum of (a1,b1) [For N-D]
		Length of Projection of one Vector on another Vector










