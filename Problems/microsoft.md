3377. Digit Operations to Make Two Integers Equal - medium

You are given two integers n and m that consist of the same number of digits. You can perform the following operations any number of times:

Choose any digit from n that is not 9 and increase it by 1. Choose any digit from n that is not 0 and decrease it by 1.
The integer n must not be a prime number at any point, including its original value and after each operation.
The cost of a transformation is the sum of all values that n takes throughout the operations performed.
Return the minimum cost to transform n into m. If it is impossible, return -1.

Example 1:
Input: n = 10, m = 12
Output: 85

Explanation:
We perform the following operations:
Increase the first digit, now n = 20.
Increase the second digit, now n = 21.
Increase the second digit, now n = 22.
Decrease the first digit, now n = 12.

Approach - Dijkshtra's Algorithm - We could have used BSA if the cost was same but it changes as we move to nextNum.

First, we store, primenumers till 10^4 limit (requirement), then we intialize a priorityqueue (min-heap with cost). We convert the n to a String, do +- combination for first digit, second digit and so on. 
For each number, we compute the total cost (previous + number value), whenever we get a number == m, return its cost.

public int minOperations(int n, int m) {
        int MAX = 10001;
        boolean [] isPrime = sieve();
        int [] dist = new int[MAX;
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[n] = n;
        PriorityQueue<int []> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        pq.add(new int [] {n, n});
        HashSet<Integer> visited = new HashSet<>();
        while( !pq.isEmpty() ){
            int[] curr = pq.poll();
            int num = curr[0];
            int cost = curr[1];
            if(visited.contains(num) || isPrime[num]) continue;
            if(num == m) return cost;
            visited.add(num);
            StringBuilder sb = new StringBuilder(Integer.toString(num));
            for(int i = 0; i<sb.length(); i++){
                char c = sb.charAt(i);
                if(c != '9'){
                    sb.setCharAt(i, (char)( c + 1));
                    int nextNum = Integer.parseInt(sb.toString());
                    int newCost = cost + nextNum;
                    if(!isPrime[nextNum] && dist[nextNum] > newCost) {
                        dist[nextNum] = newCost;
                        pq.add(new int[] { nextNum, newCost});
                    }
                    sb.setCharAt(i,c);
                }
                if ( c!= '0') {
                    sb.setCharAt(i, (char)(c - 1));
                    int nextNum = Integer.parseInt(sb.toString());
                    int newCost =cost + nextNum;
                    if(!isPrime[nextNum] && dist[nextNum] > newCost) {
                        dist[nextNum] = newCost;
                        pq.add(new int [] {nextNum, newCost});
                    }
                    sb.setCharAt(i,c);
                }
            }
        }
        return -1;
    }
    private boolean[] sieve(){
        int MAX = 10001;
        boolean [] isPrime = new boolean[MAX];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false;
        for(int i = 2; i < MAX; i++){
            if(isPrime[i]){
                for(int j = i+i; j<MAX; j+=i){
                    isPrime[j] = false;
                }
            }
        }
        return isPrime;
    }
