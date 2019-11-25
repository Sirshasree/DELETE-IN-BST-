# DELETE-IN-BST- 

import java.util.*; 

public class delete_BST {
	public static class BinarySearchTree 
	{ 
	    /* Class containing left and right child of current node and key value*/
	    public static class Node 
	    { 
	        int key; 
	        Node left, right; 
	  
	        public Node(int item) 
	        { 
	            key = item; 
	            left = right = null; 
	        } 
	    } 
	  
	    // Root of BST 
	    static Node root; 
	  
	    // Constructor 
	    BinarySearchTree() 
	    { 
	        root = null; 
	    } 
	    public static  void BST(int []arr1, int []arr2){ 
			root=construct(arr1, 0, arr1.length-1); 
			//int []a=new int[arr.length];
			//preorder(root, a, 0);
			//return a; 
			deleteKey(arr2); 
		} 
		
		private static Node construct(int []arr, int lo, int hi){
			if(lo>hi){
				return null;
			}
			//mid
			int mid=(lo+hi)/2;
			
			Node nn= new Node(arr[mid]); 
			nn.key=arr[mid];
			//System.out.print(arr[mid]+" "); 
			nn.left=construct(arr, lo, mid-1); 
			nn.right=construct(arr, mid+1, hi); 
			
			return nn; 
			
		}
		
	  
	   // This method mainly calls deleteRec() 
	    public static void deleteKey(int []arr2) 
	    { 
	       for(int i=0; i<arr2.length; i++){
	    		 root = deleteRec(root, arr2[i]);  
	    	}
	       preorder(root); 
		}
	    public static void preorder(Node node){
	   		if(node==null){
	   			return;
	   		}
	   		System.out.print(node.key+" ");  
	   		preorder(node.left);
	   		preorder(node.right);
	   		return; 
	       }
	   		
	   
	  
	    /* A recursive function to insert a new key in BST */
	    public static Node deleteRec(Node root, int key) 
	    { 
	        /* Base Case: If the tree is empty */
	        if (root == null)  return root; 
	  
	        /* Otherwise, recur down the tree */
	        if (key < root.key) 
	            root.left = deleteRec(root.left, key); 
	        else if (key > root.key) 
	            root.right = deleteRec(root.right, key); 
	  
	        // if key is same as root's key, then This is the node 
	        // to be deleted 
	        else
	        { 
	            // node with only one child or no child 
	            if (root.left == null) 
	                return root.right; 
	            else if (root.right == null) 
	                return root.left; 
	  
	            // node with two children: Get the inorder successor (smallest 
	            // in the right subtree) 
	            root.key = minValue(root.right); 
	  
	            // Delete the inorder successor 
	            root.right = deleteRec(root.right, root.key); 
	        } 
	  
	        return root; 
	    } 
	  
	    public static int minValue(Node root) 
	    { 
	        int minv = root.key; 
	        while (root.left != null) 
	        { 
	            minv = root.left.key; 
	            root = root.left; 
	        } 
	        return minv; 
	    } 
	   
	} 
	public static void main(String[] arg){
		Scanner sc=new Scanner(System.in);
		int n=sc.nextInt(); 
		int m=sc.nextInt(); 
		int []arr1=new int[n]; 
		for(int i=0; i<n; i++){ 
			arr1[i]=sc.nextInt(); 
		} 
		Arrays.sort(arr1);
		int []arr2=new int[m]; 
		for(int i=0; i<m; i++){
			arr2[i]=sc.nextInt(); 
		}
		BST(arr1, arr2);  
		
	}
}
