# A game "Xonix" which I worked on in my semester project.
It's a game, based on the tiles building while the block is moving which building new tiles. It is a C++ program including the SFML library.
## Features
- Building new tiles
- Adding the scores
- Dodging the enemies
- Different Levels
- Increase speed after 20 seconds
- Addition of Power Ups
- Score Board

## Levels
- Easy level: 2 enemies
- Medium level: 4 enemies
- Hard level: 6 enemies
- Continuous level: Addition of 2 enemies after each 20 seconds

## Concepts used
- Arrays
- Pointers
- Loops
- Conditional statements
- And basic C++ concepts

## Sample C++ code
#include <SFML/Graphics.hpp>
#include <time.h>
using namespace sf;

const int M = 25;
const int N = 40;

int grid[M][N] = {0};
int ts = 18; //tile size

struct Enemy
{int x,y,dx,dy;

  Enemy()
   {
    x=y=300;
    dx=4-rand()%8;
    dy=4-rand()%8;
   }

  void move()
   { 
    x+=dx; if (grid[y/ts][x/ts]==1) {dx=-dx; x+=dx;}
    y+=dy; if (grid[y/ts][x/ts]==1) {dy=-dy; y+=dy;}
   }
};

void drop(int y,int x)
{
  if (grid[y][x]==0) grid[y][x]=-1;
  if (grid[y-1][x]==0) drop(y-1,x);
  if (grid[y+1][x]==0) drop(y+1,x);
  if (grid[y][x-1]==0) drop(y,x-1);
  if (grid[y][x+1]==0) drop(y,x+1);
}

int main()
{
    srand(time(0));

    RenderWindow window(VideoMode(N*ts, M*ts), "Xonix Game!");
    window.setFramerateLimit(60);

    Texture t1,t2,t3;
    t1.loadFromFile("images/tiles.png");
    t2.loadFromFile("images/gameover.png");
    t3.loadFromFile("images/enemy.png");

    Sprite sTile(t1), sGameover(t2), sEnemy(t3);
    sGameover.setPosition(100,100);
    sEnemy.setOrigin(20,20);

    int enemyCount = 4;
    Enemy a[10];

    bool Game = true;
    bool menu = true;
    int x=0, y=0, dx=0, dy=0;
    float timer=0, delay=0.07; 
    Clock clock;
    text menutext;
    for (int i=0;i<M;i++)
     for (int j=0;j<N;j++)
      if (i==0 || j==0 || i==M-1 || j==N-1)  grid[i][j]=1;

    while (window.isOpen())
    {
        float time = clock.getElapsedTime().asSeconds();
        clock.restart();
        timer+=time;

        Event e;
        while (window.pollEvent(e))
        {
            if (e.type == Event::Closed)
                window.close();
               
            if (e.type == Event::KeyPressed) {
                if (menu == true) {
                    menutext.setstring("Player 1");
                    menutext.setstring("Player 2");
                    menutext.setstring("Exit");
                    menutext.setcharacterSize(24);
                    menutext.setFillColor(Color::White);
                    menutext.setStyle(text::Bold);
                    menutext.setposition({10.f, 50.f});
                }
             if (e.key.code==Keyboard::Escape)
               {
                for (int i=1;i<M-1;i++)
                 for (int j=1;j<N-1;j++)
                   grid[i][j]=0;

                x=10;y=0;
                Game=true;
               }
            }
        }

        if (Keyboard::isKeyPressed(Keyboard::Left)) {dx=-1;dy=0;};
        if (Keyboard::isKeyPressed(Keyboard::Right))  {dx=1;dy=0;};
        if (Keyboard::isKeyPressed(Keyboard::Up)) {dx=0;dy=-1;};
        if (Keyboard::isKeyPressed(Keyboard::Down)) {dx=0;dy=1;};
     }

## Author
M.Umer Sadan 
- GitHub Profile ( https://github.com/UmerSadan/Project/edit/main/README.md )
- Linked Inn ( www.linkedin.com/in/umer-sadan-a3371a1b2 )
      
