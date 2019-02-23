# Mutt-Through-A-Maze
An animated dog will be manually navigated through a maze with food that can affect its health score and food score.
//this is code I did in Eclipse IDE and pasted in separate repositories to represent different classes
//I have separate packages for hand-drawn images to represent the dog avatar which I could not figure out how to show on github

package main;
import java.awt.BorderLayout;


import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.awt.event.MouseEvent;

import java.util.ArrayList;
import java.util.concurrent.ThreadLocalRandom;

import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

import powerUps.Food;
import powerUps.PowerUpControl;
//niki
//merged mutt 
//mutt is the original backup
public class Main implements KeyListener{

	// Set up the frame for the game
	JFrame frame;
	public static DrawPanel drawPanel;
	JLabel label;

	//Set up the window heightened with variables
	private int windowWidth = 1000;
	private int windowHeight = 740;
	
	
	//private int player1DSPEESD = 6;

	private int animationCounter = 0;
	private int currentFrame = 0;
	
	private boolean dashUP = false;
	private boolean dashDOWN = false;
	private boolean dashLEFT = false;
	private boolean dashRIGHT = false;
	private boolean shift = false;
	
	

	
	static ArrayList<Button>buttonHold = new ArrayList<Button>();

	

	//creates obj Block holding array
	static Path [][] maz2D= new Path [10][10];
	static ArrayList<Path> pathHold = new ArrayList<Path>();
	
	//crates obj Mutt and holds images
	public static ArrayList<Mutt> objectHold = new ArrayList<Mutt>();
	
	
	//making 2-D array with one thing
	//	static Path [][] testPath = new Path [1][1];
		
		//creates obj path and holds paths
		
			
			//new 2-d cont.

		//mark: create maze
		/*
		private static void prepareTestBlocks () {
			for (int i = 0; i < 1; i ++) {
				for (int j = 0; j <1; j ++) {
					Path testPath0 = new Path("WALL", Resources.sidewalk, 800, 500) ;
					testPath[j][i]= testPath0;	
				}
			}
		}
		
		*/

	//creates mazes; this bit is taken from Shana's 4/14/18 version
	private static void prepareBlock () {
		
		for (int i = 0; i<10; i++) {
			for (int j=0; j<6;j++) {
				
				if(j== 0) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;				
				}else if( (j == 5) && (i != 7) ) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;	
				}else if ((i == 0) && (j != 3)) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;	
				}else if(i == 9) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;	
				}else if (( (i == 1) || (i ==2) ) && ( (j ==1 )|| (j == 2) )) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;	
				}else if ((i == 8 ) && (j ==4 )) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else if (((i == 7) || (i == 8)) && (j == 1)) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else if(((i == 8) || (i == 7)) && (j == 2)     ) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else if ((j== 3)&& (i> 6)) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else if ((j == 4)&& (i == 3)) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else if ((i == 4) && (j > 1)) {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("WALL", Resources.sidewalk, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
				}else {
					//creates blocks to put in maze2D array
					Path maz0X = new Path("PATH", Resources.maze, 128+(i*64), 105+(j*64)); 
					//at [j][i] of maz2D the latest maz0X is put in it
					maz2D[j][i]= maz0X;
					
					
					
					int randomRull = ThreadLocalRandom.current().nextInt(0,50 );
					//shana's version has cg instead of coordinateGenerator
					/*to get some null spaces do a bigger if else with if j or i!= # then do all in the if else so there will
					be some random space
					*
					*/
					
				if (i!=1 && i!=2) {
					if (randomRull <5) {
						new Food ("Chocolate", false, maz2D[j][i].x, maz2D[j][i].y,37 ,30 );
						
					}
					else if (randomRull >=10 && randomRull <20) {
						new Food ("Avocado", false, maz2D[j][i].x, maz2D[j][i].y, 26, 44);

					} else if (randomRull >=30 && randomRull <45) {
						new Food ("Bone", false, maz2D[j][i].x, maz2D[j][i].y ,39 ,39);

					} else if (randomRull >=0 && randomRull <20) {
						new Food ("Coffee", false, maz2D[j][i].x, maz2D[j][i].y,44,44);

					}else if (randomRull >=35 && randomRull <50) {
						new Food ("Meat", false, maz2D[j][i].x, maz2D[j][i].y ,30 ,36);

					}
					
					
			}
					
				}
			}
		}
		
		
		
		
		
		
		
	}
	

	public static void main(String[] args) {
		Resources.load();
		//prepareResources(); all it is in mutt
		
		System.out.println(" resources Loaded sucessfully.");
		init();
		System.out.println("init Loaded sucessfully.");

		new Main().prepareGui();
			
	}
		

	public static boolean detectFood(Mutt targetA, Food targetB) {
		//a is dog avatar, b is object from other class
		//System.out.println(targetA.x + " " + targetA.y + " " + targetB.x + " " + targetB.y);
		
		if (targetA.x < targetB.x +targetB.width &&
				targetA.x + targetA.width > targetB.x &&
				targetA.y < targetB.y + targetB.height &&
				targetA.height + targetA.y > targetB.y) {
			System.out.print("food collision is a yes.");
			
			return true;
		} else {
			return false;
		}
		
		
		
		
	}
	

	
		private static boolean detect(Mutt targetA, Path targetB) {
			//a is dog avatar, b is object from other class
			if (  (targetA.x < targetB.x +targetB.width) 
					&& (targetA.x+1 + targetA.width > targetB.x)
					&& (targetA.y< targetB.y + targetB.height)
					&& (targetA.height + targetA.y > targetB.y)) {
				System.out.print("wall collision is a yes.");
				
				return true;			
			}
			else {
				return false;
			}
			
			
			
		}
	
	private static void init() {
		prepareBlock();
		prepareMutt();
		
		prepareButton();
		
	//	preparePath();
	}
	
private static void prepareButton() {
		//start button
		Button buttonObject = new Button("Start_Button", 400 , 20, 50, 50, Resources.bluesquare, Resources.sitting);
		
	}



	private static void prepareMutt() {
		Mutt player = new Mutt("PLAYER", 50, 150, 10,10, 20, 40);
		//how to change width and height so the detect can look at the boundaries and not go over or before? 4/14
		objectHold.add(player);
		
		
	}
	
	
	private void prepareGui() {
		frame = new JFrame("MUTT");
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
		/*
		 * create a instance of the DrawPanel, it's paint-able (the Paint Class)
		 * 		 camel case means the first letter of the first word is lower case, and
  		 *		bactrian style is both first letters of the words are capitalized
		 */
		
		drawPanel = new DrawPanel();
		frame.getContentPane().add(BorderLayout.CENTER, drawPanel);
		frame.setResizable(false);
		
		drawPanel.setFocusable(true);
		drawPanel.requestFocusInWindow();
		
		drawPanel.addKeyListener(this);
				
		frame.setSize(windowWidth, windowHeight);
		frame.setLocationByPlatform(true);
		frame.setVisible(true);
		
		update();
		
	}	
	
	
	private void update() {
		
		while(true) {
	
			//affects distance/speed of the dog traveling. 
			
			if (dashUP && objectHold.get(0).y > 0) {
		
				objectHold.get(0).y -= 1;
					
				//	System.out.println("Up");
			}
			else if (dashDOWN && objectHold.get(0).y < 600){
				
				objectHold.get(0).y += 1;	
					//System.out.println("Down");	
			}
			else if (dashLEFT && objectHold.get(0).x > 0) {
				
				objectHold.get(0).x -= 1;
				//	System.out.println("Left");
			}
			else if (dashRIGHT && objectHold.get(0).x < 900) {
				
				objectHold.get(0).x += 1;
					//System.out.println("Right");	
			}
			
			
			
	// i is for columns
	for (int i = 0; i<10; i++) {
							
		//j is for rows
		for (int j=0; j<6;j++) {
								
				if (detect(objectHold.get(0), maz2D[j][i] ) ==true && maz2D[j][i].pathName=="WALL") {
						//if(maz2D[j][i].pathName=="WALL") {
							//simply put, this affects the "jumpiness" of dog. At zero, it doesn't interact with the walls at all. 
							//the higher you go numerically wise, the more "jumpy"
								if(objectHold.get(0).x < maz2D[j][i].x) {
									objectHold.get(0).x -= 1;	
										}
								if(objectHold.get(0).x > maz2D[j][i].x) {
									objectHold.get(0).x += 1;	
										}
								if(objectHold.get(0).y < maz2D[j][i].y) {
									objectHold.get(0).y -= 1;	
										}
								if(objectHold.get(0).y > maz2D[j][i].y) {
									objectHold.get(0).y += 1;	
										}
										
									//}
								}
								
							}
			}
			
			
			
			
			
				if(animationCounter < 15) {
					//six is the sweet speed
					animationCounter += 1;
				} else {
					animationCounter = 0;
					currentFrame += 1;
				}	
				
				
				
			
				if (dashRIGHT ==true && shift==true) {
					if(currentFrame >4) {
						currentFrame = 0;
					}
				} else if (dashLEFT ==true && shift==true) {
					if(currentFrame > 5) {
						currentFrame = 0;
					}
				} else if (dashUP ==true && shift==true){
					if(currentFrame > 4) {
						currentFrame = 0;
					}
				} else if (dashDOWN ==true && shift==true) {
					if(currentFrame > 5) {
						currentFrame = 0;
					}
				} else if (dashRIGHT ==true && shift ==false) {
					if(currentFrame >6) {
						currentFrame = 0;
					}
				} else if (dashLEFT ==true && shift ==false) {
					if(currentFrame > 7) {
						currentFrame = 0;
					}
				} else if (dashUP ==true && shift ==false){
					if(currentFrame >3) {
						currentFrame = 0;
					}
				} else if (dashDOWN ==true && shift ==false) {
					if(currentFrame > 5) {
						currentFrame = 0;
					}
				} else if (dashDOWN == false && dashUP ==false && dashRIGHT ==false && dashLEFT ==false) {
					if (currentFrame>3) {
						currentFrame = 0;
					}
				}
				for (int u = 0; u < PowerUpControl.powerUpList.size(); u++ ) {
					PowerUpControl.powerUpList.get(u).update();
				}
			try {
				Thread.sleep(10);				
			}
			catch (Exception e) {
				e.printStackTrace();			
			}
			
			// after sleeping, repaint the image :)
			frame.repaint();
			
			
		} //end of the while loop
		
	}


	public class DrawPanel extends JPanel {
		
		private static final long serialVersionUID = -235408667501714478L;
		
		public void paintComponent(Graphics g) {
			g.setColor(Color.BLACK);
			g.fillRect(0, 0, this.getWidth(), this.getHeight());
			
			g.setColor(Color.WHITE);
			g.drawString("Shift + arrow: run", windowWidth-200, 30);
			g.drawString("arrows: direction walking", windowWidth-200, 50);
			
			g.drawString("Health Score", windowWidth-430, 30);
			g.drawString(Integer.toString(objectHold.get(0).health), windowWidth-400, 50);
			//g.drawString("Food Score", windowWidth-300, 30);
			//g.drawString(Integer.toString(objectHold.get(0).foodCount), windowWidth-500, 50);

			
			
			//blue square
			g.drawImage(buttonHold.get(0).image, buttonHold.get(0).x, buttonHold.get(0).y,buttonHold.get(0).width, buttonHold.get(0).height, null);
			
			// i is for columns
			for (int i = 0; i<10; i++) {
							
			//j is for rows
				for (int j=0; j<6;j++) {
					//mark: draw maze
					g.drawImage(maz2D[j][i].image, maz2D[j][i].x, maz2D[j][i].y, maz2D[j][i].width, maz2D[j][i].height, null );
									
							}
			}
			

			
			/*
			g.drawImage(foodsG.get(0).foodGood.get(0), foodsG.get(0).x,foodsG.get(0).y ,  null);
			//first good food is strawberry
			g.drawImage(foodsG.get(1).foodGood.get(1), foodsG.get(1).x,foodsG.get(1).y ,  null);
			//second is meat
			g.drawImage(foodsG.get(2).foodGood.get(2), foodsG.get(2).x,foodsG.get(2).y ,  null);
			//third is fish
			g.drawImage(foodsB.get(0).foodDeath.get(0), foodsB.get(0).x, foodsB.get(0).y,null);
			//first is chocolate
			g.drawImage(foodsB.get(1).foodDeath.get(1), foodsB.get(1).x, foodsB.get(1).y, 57,41,null);
			//second is bottle aka alcohol
			g.drawImage(foodsB.get(2).foodDeath.get(2), foodsB.get(2).x, foodsB.get(2).y,  null);
			// third is coffee
			
			
			g.drawImage(foodsB.get(0).foodIrritation.get(0), foodsB.get(0).x, foodsB.get(0).y, null);
			//avocado above
			g.drawImage(foodsB.get(1).foodIrritation.get(1), 600, 363, 20,32, null);
			//citrus above
			*/

			
			
			if (dashRIGHT ==true && shift==false) {
				//E walking
				g.drawImage(objectHold.get(0).resListEW.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, null);
					
				objectHold.get(0).direction = "EAST";
			} else if (dashRIGHT == true && shift ==true){
				//E running
				g.drawImage(objectHold.get(0).resListER.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "EAST";
			} else if (dashLEFT ==true && shift ==false) {
				//W walk
				g.drawImage(objectHold.get(0).resListWW.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "WEST";
			} else if(dashLEFT==true && shift ==true) {
				//W running
				g.drawImage(objectHold.get(0).resListWR.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "WEST";
			} else if(dashUP == true && shift ==true) {
				//N running
				g.drawImage(objectHold.get(0).resListNR.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, null);
				objectHold.get(0).direction = "NORTH";
			} else if(dashUP == true && shift ==false) {
				//N walking
				g.drawImage(objectHold.get(0).resListNW.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "NORTH";
			} else if(dashDOWN == true && shift ==true) {
				//S running
				g.drawImage(objectHold.get(0).resListSR.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "SOUTH";
			} else if(dashDOWN == true && shift ==false) {
				//S running
				g.drawImage(objectHold.get(0).resListSW.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y,  null);
				objectHold.get(0).direction = "SOUTH";
				//from here this deals with sitting positions
			} else if (dashDOWN == false && objectHold.get(0).direction =="WEST") {
				g.drawImage(objectHold.get(0).sittingW.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, 55, 40,   null);

			} else if (dashDOWN == false && objectHold.get(0).direction =="EAST") {
				g.drawImage(objectHold.get(0).sittingE.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, 55, 40,   null);

			} else if (dashDOWN == false && objectHold.get(0).direction =="NORTH") {
				g.drawImage(objectHold.get(0).sittingN.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, 15, 40,  null);

			} else if (dashDOWN == false && objectHold.get(0).direction =="SOUTH") {
				g.drawImage(objectHold.get(0).sittingS.get(currentFrame), objectHold.get(0).x, objectHold.get(0).y, 22,40, null);

			} else {
				System.out.println("If-else statement for drawing dog is not working");				
			}
			
			for (int r = 0; r < PowerUpControl.powerUpList.size(); r++) {
				PowerUpControl.powerUpList.get(r).render(g);
			}
			
	}
	
	
	
	
}

	public void mouseMoved(MouseEvent e) {
			//System.out.println(e.getX());
			//System.out.println(e.getY());
	}
	
	
	
	public void mouseReleased(MouseEvent e) {
		
		
		
		//find way to get button working
	//	System.out.println(e.getX());
		//System.out.println(e.getY());
}

	
	@Override
	public void keyPressed(KeyEvent e) {

		try {
			Thread.sleep(10);
		}
		catch (Exception ex) {
			ex.printStackTrace();
		}
		
		if (e.getKeyCode() == KeyEvent.VK_RIGHT) {
			
			dashRIGHT = true;
		}
		else if (e.getKeyCode() == KeyEvent.VK_LEFT) {
			dashLEFT = true;
		}
		else if (e.getKeyCode() == KeyEvent.VK_DOWN) {
			dashDOWN = true;			
		}
		else if (e.getKeyCode() == KeyEvent.VK_UP) {
			dashUP = true;
		}
		else if (e.getKeyCode() == KeyEvent.VK_SHIFT) {
			shift = true;
		}
		
	}



	@Override
	public void keyReleased(KeyEvent e) {
		try {
			Thread.sleep(10);
		}
		catch (Exception ex) {
			ex.printStackTrace();
		}
		
		if (e.getKeyCode() == KeyEvent.VK_RIGHT) {
			dashRIGHT = false;
		}
		else if (e.getKeyCode() == KeyEvent.VK_LEFT) {
			dashLEFT = false;
		}
		else if (e.getKeyCode() == KeyEvent.VK_DOWN) {
			dashDOWN = false;			
		}
		else if (e.getKeyCode() == KeyEvent.VK_UP) {
			dashUP = false;
		}
		else if (e.getKeyCode() == KeyEvent.VK_SHIFT) {
			shift = false;
		}
		
		
	}


	@Override
	public void keyTyped(KeyEvent arg0) {
		// TODO Auto-generated method stub
		
	}
	
}
