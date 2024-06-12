### [나의 답]

```java
import java.io.*;
import java.util.*;

class Main {
	static int N;
	static String map[][];
	static int moveR[] = {-1, 1, 0, 0};
	static int moveC[] = {0, 0, 1, -1}; // U, D, R, L
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st;
		
		N = Integer.parseInt(br.readLine());
		map = new String[N + 1][N + 1];
		
		st = new StringTokenizer(br.readLine());
		int goormR = Integer.parseInt(st.nextToken());
		int goormC = Integer.parseInt(st.nextToken());
		st = new StringTokenizer(br.readLine());
		int playerR = Integer.parseInt(st.nextToken());
		int playerC = Integer.parseInt(st.nextToken());
		
		for (int i = 1; i <= N; i++) {
			st = new StringTokenizer(br.readLine());
			for (int j = 1; j <= N; j++) {
				map[i][j] = st.nextToken();
			}
		}
		
		int goormCount = play(goormR, goormC);
		int playerCount = play(playerR, playerC);
		if (goormCount > playerCount) {
			System.out.println("goorm " + goormCount);
		} else {
			System.out.println("player " + playerCount);
		}
		
	}
	
	public static int play(int startR, int startC) {
		int totalCount = 0;
		int currentR = startR;
		int currentC = startC;
		boolean visited[][] = new boolean[N + 1][N + 1];
		visited[currentR][currentC] = true;
		totalCount++;
		boolean isPlay = true;
		
		while (isPlay) {
			String order = map[currentR][currentC];
			int count = Integer.parseInt(order.substring(0, order.length() - 1));
			int direction = getDirection(order.substring(order.length() - 1).charAt(0));
			
			while (count-- > 0) {
				int nextR = currentR + moveR[direction];
				int nextC = currentC + moveC[direction];
				
				if (nextR <= 0) nextR = N;
				if (nextC <= 0) nextC = N;
				if (nextR > N) nextR = 1;
				if (nextC > N) nextC = 1;
				
				if (visited[nextR][nextC]) {
					isPlay = false;
					break;
				}
				
				currentR = nextR;
				currentC = nextC;
				visited[currentR][currentC] = true;
				totalCount++;
			}
			
		}
		
		return totalCount;
	}
	
	static int getDirection(char command) {
		if (command == 'U') return 0;
		if (command == 'D') return 1;
		if (command == 'R') return 2;
		if (command == 'L') return 3;
		return -1;
	}
	
}

=> 문제 조건 잘 인지하기
```
