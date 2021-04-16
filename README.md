Q.1. You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

class Solution {
    public int coinChange(int[] coins, int amount) {
        
        int n=0;int c=0;int a=0;int temp=0;int arr[][]=new int[coins.length][amount+1];
        n=coins.length;
        a=n-1;
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n-1;j++)
            {
                if(coins[j+1]<coins[j])
                {
                    temp=coins[j];
                    coins[j]=coins[j+1];
                    coins[j+1]=temp;
                }
           }
        }
    /*      for(int k=0;k<n;k++)
              arr[k][0]=0;
        for(int l=0;l<=amount;l++)
        {
            if(l%coins[0]==0)
            arr[0][l]=l/coins[0];
            else
                arr[0][l]=0;
        }
        for(int i=1;i<n;i++)
        {
            for(int j=1;j<=amount;j++)
            {
            if(coins[i]>j)
            {
                arr[i][j]=arr[i-1][j];
            }
                else
                    arr[i][j]=Math.min(arr[i-1][j],1+arr[i][j-coins[i]]);
                }
        }
        return arr[coins.length-1][amount];*/
        int[] dp = new int[amount+1];

		// format the int array for processing
		Arrays.fill(dp,amount+1);
		dp[0] = 0;

		// update the array with the minimum number of coins needed at each amount 
		for(int coin: coins) {
			for(int i = coin; i < dp.length; i++) {
				dp[i] = Math.min(dp[i], dp[i-coin] + 1);
			}
		}

		// return the minimum number of coins needed at the requested amount
		int minCoins = dp[dp.length-1];
		return dp[dp.length-1] == amount+1 ? -1 : minCoins;
    }
}
