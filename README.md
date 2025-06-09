import java.awt.Color;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Rectangle;
import java.awt.event.KeyEvent;
import java.util.ArrayList;

import javax.swing.JPanel;

public class GraphicsPanel extends JPanel {


    public GraphicsPanel() {
        setPreferredSize(new Dimension(500, 500));
    }

    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        Graphics2D g2 = (Graphics2D) g;

        int centerX = getWidth() / 2;
        int centerY = getHeight() / 2;

       
}




    private Timer timer;
    private Background background;
    private Sprite sprite;

    private Timer timer;
    private Background background;
    private Sprite sprite; 
    
    private final int GRAVITY = 1;
    private final int JUMP_STRENGTH = -12;
    private int velocityY = 0; 
    
    private final int GROUND_LEVEL = 400;
    private final int PIPE_WIDTH = 60; 
    private final int PIPE_GAP = 150; 
    private final int PIPE_SPACING = 300; 
    private final int PIPE_ArrayList<E>;
    
    private ArrayList<Rectangle> pipes; 
    private Random rand;
    
    public GraphicsPanel() {
    	background = new ForestBackground(); 
    	sprite = new Girl (50,200);
    setPreferredSize(new Dimension(background.getWidth(), background.getHeight()));
    setFocusable(true);
    addKeyListener(this); 
    
    pipes = new ArrayList<>();
    rand = new Random ();
    //code for initial pipes
    for (int i = 0; i < 3; i++) {
    	addPipe(600 + i * PIPE_SPACING);
    	
    }
    timer = new Timer(15, new ClockListener());
    timer.start(); 
    
    }
    public void paintComponent(Graphics g) {
    	super.paintComponent(g);
    	Graphics2D g2 = (Graphics2D) g;
    	
    	background.draw(this,  g);
    	sprite.draw(g2, this);
    	
    	g2.setColor(Color.GREEN);
    	for (Rectangle pipe: pipes) {
    		g2.fill(pipe);
    	
    	}
    }
    public void clock() {
    	//grv
    	velocityY += GRAVITY;
    	sprite.y_coordinate += velocityY;
    	//dont go below floor
    	if (sprite.y_coordinate > GROUND_LEVEL) {
    		sprite.y_coordinate = GROUND_LEVEL; 
    		velocityY= 0; 
    	}
    }
   //move p
    for (int i = 0; i < pipes.size(); i++) {
    	Rectangle pipe = pipes.get(i); 
    	pipe.x -= PIPE_SPEED;
    	
    }
    //remove pipes from screen+new ones
    if (!pipes.isEmpty() && pipes.get(0).x + PIPE_WIDTH < 0) {
    	pipes.remove(0); 
    	pipes.remove(0); 
    	addPipe(pipes.get(pipes.size() - 1).x + PIPE_SPACING);
    }
    for (Rectangle pipe : pipes) {
    	if (pipe.intersects(sprite.getBounds())) {
    		sprite.die(); 
    	}
    }
    repaint();
    
    }
    
    private void addPipe(int x) {
    	int height = 100 + rand.nextInt(200);
    	pipes.add(new Rectangle(x, 0, PIPE_WIDTH, height)); //top
    	pipes.add(new Rectangle(x, height + PIPE_GAP, PIPE_WIDTH, background.getHeight()));
    }
    
   public void keyPressed(KeyEvent e) {
	   int code = e.getKeyCode();
	   if (code == KeyEvent.KEY_FIRST VK_SPACE || code == keyEvent.VK_UP) {
		   velocityY = JUMP_STRENGTH;
	   }else if (code == KeyEcent.VK_DOWN ) {
		   sprite.y_coordinate += 10; //not required
	   }
   }
   public void keyReleased(KeyEvent e) {  }
   
   public void keyTyped(KeyEvent e) { }
   
   private class ClockListener implements ActionListener {
	   public void actionPerformed(ActionEvent e) {
		   clock (); 
	   }
   }
   }
    
