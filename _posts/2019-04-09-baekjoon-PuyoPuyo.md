---
title:  "[backjoon] 11559. Puyo Puyo"
categories: [algorithm]
tags: algorithm, BFS, 시뮬레이션
author: myxxxxme
---

### 문제
https://www.acmicpc.net/problem/11559

### [1] Answer Code (19. 04. 09)
import java.awt.Point;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
	static char[][] map = new char[12][6];
	static int[][] dir = {{0,1},{1,0},{0,-1},{-1,0}};
	static int ans;
	static boolean flag;

	public static void dump() {
	
		int tmpi, tmpidx = 0;
		for(int j=0; j<6; j++) {
			for(int i=11; i>=0; i--) {
				
				tmpidx = 0;
				tmpi = i;
				while(tmpi>=0 && (map[tmpi][j]=='0')) {
					tmpidx++;
					--tmpi;
				}
				
				for(int c=0; c<tmpidx; c++) {
					if(tmpi-c>=0) {
					map[tmpi+tmpidx-c][j] = map[tmpi-c][j];
					
					if(map[tmpi-c][j] != '.')
						map[tmpi-c][j] = '0';
					}
				}
				
			}
		}
		ans+=1;
	}
	
	public static void searchSameColor() {
		char color;
		Queue<Point> que;
		boolean[][] visited =  new boolean[12][6];

		for(int i=11; i>=0; i--) {
			for(int j=0; j<6; j++) {
				if(!visited[i][j] && map[i][j]!='.' && map[i][j]!='0') {
					color = map[i][j];
					que = new LinkedList<>();
					que.add(new Point(i,j));
					visited[i][j] = true;

					LinkedList<Point> list = new LinkedList<>();
					list.add(new Point(i,j));
					int colorcnt=1;

					while(!que.isEmpty()) {

						Point tmp = que.poll();
						int nextr, nextc;

						for(int d=0; d<4; d++) {
							nextr = tmp.x + dir[d][0];
							nextc = tmp.y + dir[d][1];

							if(nextr < 0 || nextc < 0 || nextr >= 12 || nextc >=6 || visited[nextr][nextc])
								continue;

							if(map[nextr][nextc] == color) {
								colorcnt++;
								list.add(new Point(nextr, nextc));
								que.add(new Point(nextr, nextc));
								visited[nextr][nextc] = true;
							}
			
						}
					}	

					if(colorcnt >=4 ) {
						flag = true;
						for(int l=0; l<list.size(); l++) {
							Point tmpremove = list.get(l);
							map[tmpremove.x][tmpremove.y] = '0';
						}
					}
				}
			}

		}

	}

	

	public static void print() {

		System.out.println();

		for(int i=0; i<12; i++) {
			System.out.println();
			for(int j=0; j<6; j++) {
				System.out.print(map[i][j]);
			}
		}
	}

	

	public static void main(String[] args) throws IOException{

		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		for(int i=0; i<12; i++) {
			map[i] = br.readLine().toCharArray();
		}
		
		ans = 0;
		flag = false;
		searchSameColor();
		while(flag) {
			dump();
			//print();
			flag = false;
			searchSameColor();
		}
		System.out.println(ans);

	}



}


```
