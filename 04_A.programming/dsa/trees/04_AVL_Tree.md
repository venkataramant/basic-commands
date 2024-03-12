# AVL Tree or Balance BST

# Height
	h(None)			= -1
	h(singleNode)	=  0
	h(Node) 			= 1+ max(h(left_node),h(right_node))

# Balance of Node
	balance(Node)	= H(left_node)-H(right_node)
	
	AVL Tree
	for all nodes in the Tree 
		if abs(balance(Node))<=1 
	
	Balance >0 Left_Heavy
	Balance <0 Right_Heavy

# Rotations
	Aim: To fix imbalance

	Left_Heavy
		1. Right		  (If new Node is Inserted on Left side)
		2. Left-Right (If new Node is Inserted on Right side)
	Right_heavy
		1. Left		  (If new Node is Inserted on Right side)
		2. Right-Left (If new Node is Inserted on Left side)

#