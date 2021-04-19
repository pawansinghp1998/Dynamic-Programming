Q.1. You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

class Solution {
    public int coinChange(int[] coins, int amount) {
        
        
        int[][] dp = new int[coins.length+1][amount+1];
        
        
        for(int j = 0; j < dp[0].length; ++j){
            dp[0][j]= Integer.MAX_VALUE -1; // Initializing with infinity -1             //Initiazing first roe with integer.max-1
        }
        
        for(int i = 1; i < dp.length; ++i){
            dp[i][0] = 0;                                                                 //Initializing first column with zero
        }
        
        for(int j = 1; j< dp[0].length; ++j){
            if(j % coins[0] == 0){
                dp[1][j] = j/coins[0];                                                    //Initializing the colum with no of coins needed of particular
            }else{
                dp[1][j] = Integer.MAX_VALUE -1;
            }
        }
        
        
        for(int i = 2; i < dp.length; ++i){
            for(int j = 1; j < dp[0].length; ++j){
                if(coins[i-1] > j){
                    dp[i][j]= dp[i-1][j];
                }else{
                    dp[i][j] = Math.min(1 + dp[i][j-coins[i-1]], dp[i-1][j]);         // filling the dynamic array with min no of coin needed
                }
            }
        }
        
        
        return dp[coins.length][amount] != Integer.MAX_VALUE-1 ? dp[coins.length][amount]: -1;   //if particular amount can not be achieved then return -1
    }
}



Q.2(221)Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

class Solution {
    public int maximalSquare(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int max = 0;
        int[][] dp = new int[m][n];
        
        for(int x = 0; x < m; x++) {
            for(int y = 0; y < n; y++) {
                if(matrix[x][y] == '1') {                                                        //if particular index is filled with 1.
                    if(x == 0 || y == 0){                                                        //if it is either first row or first column
                        dp[x][y] = 1;
                    }else{
                     dp[x][y] = Math.min(Math.min(dp[x-1][y], dp[x][y-1]), dp[x-1][y-1]) + 1;     //Largest posiible square at particular index
                }
                
                max = Math.max(max, dp[x][y]);                                                   // to find max value of dp array
            }  
        }
        }
        return max*max;                                                                        //returning the no of element of max possible array
    }
}



Q.3(5)Given a string s, return the longest palindromic substring in s.

class Solution {
    public String longestPalindrome(String s) {
        int n=s.length(); int max=0; String str="";
        int arr[][]=new int[n][n];
        for(int i=0;i<n;i++)
        {
            max=1;
            arr[i][i]=1;                                           \\filling all diagonal element with 1 bcz one character is always palindrome
            str=s.substring(i,i+1);
        }
        for(int j=0;j<n-1;j++)
        {
            if (s.charAt(j)==s.charAt(j+1))
            {
                max=2;
                arr[j][j+1]=1;                                     \\ filling the diagonal above pricipal diagonal
                str=s.substring(j,j+2);
                
            }
        }
        for(int k=2;k<n;k++)
        {
            for(int l=0;l<n-k;l++)
            {
                if(s.charAt(l)==s.charAt(l+k) && arr[l+1][l+k-1]==1)     \\filling if first character is equal to last character and checking middle characters with previous                                                                                    calculation
                {
                    arr[l][l+k]=1;
                    if(max<(k+1))
                    {
                        str=s.substring(l,l+k+1);
                      max=k+1;
                       }}
            }
        }
                       return str;
    }}
    
    Q.4Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

 class Solution {
    public int trap(int[] height) {
       int n=height.length;int leftmax=0;int rightmax=0;int z=0;int sum=0;
        for(int i=0;i<n;i++)
        {leftmax=0; rightmax=0;
            for(int j=i-1;j>=0;j--)
            {
               leftmax= Math.max(leftmax,height[j]);
            }
            for(int j=i+1;j<n;j++)
            {
               rightmax= Math.max(rightmax,height[j]);
            }
           z= Math.min(leftmax,rightmax)-height[i];
           if(z>0)
                sum=sum+z;
        }
        		
		    return sum;
    }
}
