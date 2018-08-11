# Battleship
//Project Battleship (using arrays in JAVA)

import java.util.*;
import java.util.Random;
public class BattleShip {
    public static void main(String[] args) {
        int[][] map = new int[10][10];
        System.out.println("******Welcome to the Battleship Game*********");
        System.out.println();
        System.out.println("Right now, the sea is empty");
        System.out.println();
        String[][] oceanMap = new String[10][10];
        String[][] playerShips = new String[10][10];
        String[][] compShips = new String[10][10];
        displayMap(map);
        userPlacesShips(map);
        computerPlacesShips(map);
        int user = 5;
        int computer = 5;
        while (!(user == 0)|| !(computer ==0)){
            displayMap(map);
            int u = userPlay(map);
            if (user == 1){
                computer--;
            }
            else user += u;
            checkWin(user,computer,map);
            int c = computerPlay(map);
            if (c == 1){
                user--;
            }
            else computer += c;
            checkWin(user,computer,map);
            System.out.println("Your Ships :"+ user+ " | Computer Ships :"+computer);
        }
        System.out.println("Sorry you didn't escape in time - you loose");
        System.exit(0);
    }
    public static void displayMap(int[][] map){
        System.out.println("   0123456789");

        for (int i = 0; i < 10; i++){
            System.out.print(i + " |");

            for (int j = 0; j < 10; j++) {
                if (map[i][j] == 0 || map[i][j] == 2 || map[i][j] == 4){
                    System.out.print(" ");
                }
                else if (map[i][j] == 1){
                    System.out.print("@");
                }
            /*
            if (map[i][j] == 2){ // This is computer's ship --> no print
                System.out.print("-");
            }
            */
                else if (map[i][j] == 3){
                    System.out.print("-");
                }
                else if (map[i][j] == 11 || map[i][j] == 12){
                    System.out.print("x");
                }
                else if (map[i][j] == 21 || map[i][j] == 22) {
                    System.out.print("!");
                }
            }
            System.out.println("| " + i);
        }

        System.out.println("   0123456789");
    }


    public static void userPlacesShips(int[][]map){
        Scanner input = new Scanner(System.in);
        for (int i =0;i<=5;i++){
            System.out.print("Enter X coordinate for ship "+i+": ");
            int x = input.nextInt();
            System.out.print("Enter Y coordinate for ship "+i+": ");
            int y = input.nextInt();
            if (map[x][y]==0){
                map[x][y]= 1;
            }
            else{
                System.out.println("You already have a ship at position: "+x+", "+y);
                i--;
            }
        }


    }
    public static void computerPlacesShips(int[][] map){
        System.out.println();
        System.out.println("Computer is deploying ship");
        Random random = new Random();
        for (int i=1;i<=5;i++){
            int x = random.nextInt(10);
            int y = random.nextInt(10);
            if (map[x][y]==0){
                map[x][y]=2;
            }
            System.out.println(i + " Ship deployed");
        }
        System.out.println("--------------------------------------------------");
    }
    public static int userPlay(int [][] map){
        System.out.println("Your Turn");
        Scanner input = new Scanner(System.in);
        System.out.println("Enter X coordinate: ");
        int x = input.nextInt();
        System.out.println("Enter Y coordinate: ");
        int y = input.nextInt();
        if (x<0||x>9|| y<0||y>9){
            System.out.println("You must play a position within grid (0-9");
            System.out.println();
            return userPlay(map);
        }
        if (map [x][y] == 1){
            map[x][y]= 11;
            System.out.println("oh no, you sunk your own ship :(");
            System.out.println();
            return -1;
        }
        else if (map[x][y]== 2){
            map[x][y]= 21;
            System.out.println("BOOM!! you sunk the ship!");
            System.out.println();
            return 1;

        }
        else if (map[x][y]== 3|| map[x][y]== 11|| map[x][y]== 21){
            System.out.println("You already played that position.");
            System.out.println();
            return userPlay(map);

        }
        else if (map[x][y]> 4){
            System.out.println("This position was already played.");
            System.out.println();
            return userPlay(map);
        }
        else {
            map[x][y] = 3;
            System.out.println("Sorry you missed.");
            System.out.println();
            return 0;
        }
    }
    public static int computerPlay(int[][] map){
        System.out.println("Computer's turn");
        Random random = new Random();
        int x = random.nextInt(10);
        int y = random.nextInt(10);
        if (map [x][y]==1){
            map[x][y] = 12;
            System.out.println("BOOM!! Computer sunk your ship!!");
            System.out.println();
            return 1;
        }
        else if (map[x][y]==2){
            map[x][y]= 22;
            System.out.println("Computer sunk his own ship! ");
            System.out.println();
            return -1;
        }
        else if (map[x][y]>= 4){
            return computerPlay(map);
        }
        else {
            System.out.println("Computer missed.");
            System.out.println();
            return 0;
        }
    }
    public static void checkWin(int user, int comp, int[][] map){
        if (user==0){
            displayMap(map);
            System.out.println("Sorry, computer won the battle.");
            System.exit(0);
        }
        if (comp==0){
            displayMap(map);
            System.out.println("Congrats!!! You won the battle.");
            System.exit(0);
        }

    }
}


