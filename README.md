 public class BinarySearchTree< AnyType extends Comparable<? super AnyType> >
	{
	    /**
	     * Construct the tree.
	     */
	    public BinarySearchTree( )
	    {
	        root = null;
	    }

	    /**
	     * Insert into the tree; duplicates are ignored.
	     * @param x the item to insert.
	     */
	    public void insert( AnyType x )
	    {
	        root = insert( x, root );
	    }

	    /**
	     * Remove from the tree. Nothing is done if x is not found.
	     * @param x the item to remove.
	     */
	    public void remove( AnyType x )
	    {
	        root = remove( x, root );
	    }

	    /**
	     * Find the smallest item in the tree.
	     * @return smallest item or null if empty.
	     */
	    public AnyType findMin( )
	    {
	        if( isEmpty( ) )
	            throw new UnderflowException( );
	        return findMin( root ).element;
	    }

	    /**
	     * Find the largest item in the tree.
	     * @return the largest item of null if empty.
	     */
	    public AnyType findMax( )
	    {
	        if( isEmpty( ) )
	            throw new UnderflowException( );
	        return findMax( root ).element;
	    }

	    /**
	     * Find an item in the tree.
	     * @param x the item to search for.
	     * @return true if not found.
	     */
	    public boolean contains( AnyType x )
	    {
	        return contains( x, root );
	    }

	    /**
	     * Make the tree logically empty.
	     */
	    public void makeEmpty( )
	    {
	        root = null;
	    }

	    /**
	     * Test if the tree is logically empty.
	     * @return true if empty, false otherwise.
	     */
	    public boolean isEmpty( )
	    {
	        return root == null;
	    }

	    

	    /**
	     * Internal method to insert into a subtree.
	     * @param x the item to insert.
	     * @param t the node that roots the subtree.
	     * @return the new root of the subtree.
	     */
	    private BinaryNode<AnyType> insert( AnyType x, BinaryNode<AnyType> t )
	    {
	        if( t == null )/* Create and return a one-node tree */ 
	            return new BinaryNode<>( x, null, null );
	        
	        /* If there is a tree */
	        int compareResult = x.compareTo( t.element );
	            
	        if( compareResult < 0 )
	            t.left = insert( x, t.left );
	        else if( compareResult > 0 )
	            t.right = insert( x, t.right );
	        else
	            ;  // Duplicate; do nothing
	        return t; /* Do not forget this line!! */ 
	    }

	    /**
	     * Internal method to remove from a subtree.
	     * @param x the item to remove.
	     * @param t the node that roots the subtree.
	     * @return the new root of the subtree.
	     */
	    private BinaryNode<AnyType> remove( AnyType x, BinaryNode<AnyType> t )
	    {
	        if( t == null )
	            return t;   // Item not found; do nothing
	            
	        int compareResult = x.compareTo( t.element );
	            
	        if( compareResult < 0 )
	            t.left = remove( x, t.left );
	        else if( compareResult > 0 )
	            t.right = remove( x, t.right );
	        else if( t.left != null && t.right != null ) // Two children
	        {
	            t.element = findMin( t.right ).element;
	            t.right = remove( t.element, t.right );
	        }
	        else
	            t = ( t.left != null ) ? t.left : t.right;
	        return t;
	    }

	    /**
	     * Internal method to find the smallest item in a subtree.
	     * @param t the node that roots the subtree.
	     * @return node containing the smallest item.
	     */
	    private BinaryNode<AnyType> findMin( BinaryNode<AnyType> t )
	    {
	        //recursive version
	        if( t == null )
	            return null;
	        else if( t.left == null )
	            return t;
	        return findMin( t.left );
	        
	        //iterative version
	        
	        
	    }

	    /**
	     * Internal method to find the largest item in a subtree.
	     * @param t the node that roots the subtree.
	     * @return node containing the largest item.
	     */
	    private BinaryNode<AnyType> findMax( BinaryNode<AnyType> t )
	    {
	        if( t != null )
	            while( t.right != null )
	                t = t.right;

	        return t;
	    }

	    /**
	     * Internal method to find an item in a subtree.
	     * @param x is item to search for.
	     * @param t the node that roots the subtree.
	     * @return node containing the matched item.
	     */
	    private boolean contains( AnyType x, BinaryNode<AnyType> t )
	    {
	        if( t == null )
	            return false;
	            
	        int compareResult = x.compareTo( t.element );
	            
	        if( compareResult < 0 )
	            return contains( x, t.left );
	        else if( compareResult > 0 )
	            return contains( x, t.right );
	        else
	            return true;    // Match
	    }

	   
	    
	    // Basic node stored in unbalanced binary search trees
	    private static class BinaryNode<AnyType>
	    {
	            // Constructors
	        BinaryNode( AnyType theElement )
	        {
	            this( theElement, null, null );
	        }

	        BinaryNode( AnyType theElement, BinaryNode<AnyType> lt, BinaryNode<AnyType> rt )
	        {
	            element  = theElement;
	            left     = lt;
	            right    = rt;
	        }

	        AnyType element;            // The data in the node
	        BinaryNode<AnyType> left;   // Left child
	        BinaryNode<AnyType> right;  // Right child
	    }


	      /** The tree root. */
	    private BinaryNode<AnyType> root;


	        // Test program
	    public static void main( String [ ] args )
	    {
	        BinarySearchTree<Integer> t = new BinarySearchTree<>( );
	       
	    }
}
