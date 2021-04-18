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
