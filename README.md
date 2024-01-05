# Tic-Tae-Toe
#include <bits/stdc++.h>
#include <windows.h>
#include <conio.h>
using namespace std;

struct game_board
{
    int martix[3][3];
};
struct movement
{
    int row;
    int column;
};

int who_win(game_board board, int move_no);
double utility(game_board board,int depth,int move_no);
double max_finding(game_board board, int depth, int move_no);
double min_finding(game_board board, int depth, int move_no);
double min_finding(game_board board, int depth, int move_no);
void welcome_show();
void thank_show();

int who_win(game_board board, int move_no)
{
    /** pc check
    / row check start....
    */
    if(board.martix[0][0] == 1 && board.martix[0][1]== 1 && board.martix[0][2] == 1) return 1;
    else if(board.martix[1][0] == 1 && board.martix[1][1]== 1 && board.martix[1][2] == 1) return 1;
    else if(board.martix[2][0] == 1 && board.martix[2][1]== 1 && board.martix[2][2] == 1) return 1;

    /** column check...start */
    else if(board.martix[0][0] == 1 && board.martix[1][0]== 1 && board.martix[2][0] == 1) return 1;
    else if(board.martix[0][1] == 1 && board.martix[1][1]== 1 && board.martix[2][1] == 1) return 1;
    else if(board.martix[0][2] == 1 && board.martix[1][2]== 1 && board.martix[2][2] == 1) return 1;

    /**diagonal check */
    else if(board.martix[0][0] == 1 && board.martix[1][1]== 1 && board.martix[2][2] == 1) return 1;
    else if(board.martix[2][0] == 1 && board.martix[1][1]== 1 && board.martix[0][2] == 1) return 1;

    /** player check start....
    / row check start....
    */
    else if(board.martix[0][0] == 2 && board.martix[0][1]== 2 && board.martix[0][2] == 2) return 2;
    else if(board.martix[1][0] == 2 && board.martix[1][1]== 2 && board.martix[1][2] == 2) return 2;
    else if(board.martix[2][0] == 2 && board.martix[2][1]== 2 && board.martix[2][2] == 2) return 2;

    /** column check...start */
    else if(board.martix[0][0] == 2 && board.martix[1][0]== 2 && board.martix[2][0] == 2) return 2;
    else if(board.martix[0][1] == 2 && board.martix[1][1]== 2 && board.martix[2][1] == 2) return 2;
    else if(board.martix[0][2] == 2 && board.martix[1][2]== 2 && board.martix[2][2] == 2) return 2;

    /**diagonal check */
    else if(board.martix[0][0] == 2 && board.martix[1][1]== 2 && board.martix[2][2] == 2) return 2;
    else if(board.martix[2][0] == 2 && board.martix[1][1]== 2 && board.martix[0][2] == 2) return 2;

    else if( move_no >= 9) return 0;
    else return -1;
}

double utility(game_board board,int depth,int move_no)
{
    if(who_win(board,move_no) == 1) return double(1)/depth;
    else if(who_win(board,move_no) == 2) return -1;
    else if(who_win(board,move_no) == 0) return 0;
}
double max_finding(game_board board, int depth, int move_no)
{
    if(who_win(board,move_no) == -1)
    {
        double util = -9999;
        for(int i=0;i<3;i++)
        {
            for(int j=0;j<3;j++)
            {
                if(board.martix[i][j] == 0)
                {
                    board.martix[i][j] = 1;
                    util = max(util,min_finding(board,depth+1,move_no+1));
                    board.martix[i][j] = 0;
                }
            }
        }
        return util;
    }
    else return utility(board,depth,move_no);
}

double min_finding(game_board board, int depth, int move_no)
{
    if(who_win(board,move_no) == -1)
    {
        double util = 9999;
        for(int i=0;i<3;i++)
        {
            for(int j=0;j<3;j++)
            {
                if(board.martix[i][j] == 0)
                {
                    board.martix[i][j] = 2;
                    util = min(util,max_finding(board,depth+1,move_no+1));
                    board.martix[i][j] = 0;
                }
            }
        }
        return util;
    }
    else return utility(board,depth,move_no);

}

movement choose_pc_move(game_board board, int move_no)
{
    double best = -9999;
    movement m;
    for(int i=0;i<3;i++)
    {
        for(int j=0;j<3;j++)
        {
            if(board.martix[i][j] == 0)
            {
                board.martix[i][j] = 1;
                double util = min_finding(board,1,move_no+1);
                board.martix[i][j] = 0;
                if(best<util)
                {
                    best = util;
                    m.row = i;
                    m.column = j;
                }
            }
        }
    }
    return m;
}



void welcome_show()
{
    char welcome[100] = "........Welcome to Tic Tac Toe game........";
    char loading[100] = "........LOADING........";

    int it1, it2, it3;
    for(it3 = 0; it3< 2; it3++)
    {
        cout << "\n\n\n\n\n\t\t\t";
        for(it1 = 0; loading[it1] != '\0'; it1++)
        {
            cout << loading[it1];
            for(it2 = 0; it2< 70000000; it2++){}
        }
        system("cls");
    }

    cout << "\n\n\n\n\n\t\t\t";
    for(it1 = 0; welcome[it1] != '\0'; it1++)
    {
        cout << welcome[it1];
        for(it2 = 0; it2< 50000000; it2++){}
    }

    cout << "\n\n\t\t\t\t   press any key to play\n\n\n\t\t\t\t   ";
    getch ();
}

void thank_show()
{
    char thanks[100] = "..............Thank you..............";

    int it1, it2;
    printf("\n\n\n\t\t");
    for(it1 = 0; thanks[it1] != '\0'; it1++)
    {
        cout << thanks[it1];
        for(it2 = 0; it2< 50000000; it2++){}
    }
    cout << "\n\n\t\t     ....press any key to exit....\n\n\n\t\t\t\t   ";

}

int main()
{
    welcome_show();
    redo:
    int move_no = 0;
    game_board board;
    for(int i=0;i<3;i++)
    {
        for(int j=0;j<3;j++)
        {
            board.martix[i][j] = 0;
        }
    }

    system("cls");
    cout << "\tGame Board rules";
    cout << endl << endl << endl;
    for(int i=2;i>=0;i--)
    {
        int c = i*3;
        for(int j=0;j<3;j++)
        {
            c++;
            cout << "    " ;

            cout << c;
            if(j!=2) cout << "    |";

        }
        if(i!=0) cout << "\n\n  -------------------------\n\n" ;
    }
    cout << endl << endl << endl;


    while(who_win(board,move_no) == -1)
    {
        bool pc_move = false;
        int place;
        cout << "    Make your move : " ;
        cin >> place;
        if(place == 1 && board.martix[2][0] == 0 )
        {
            board.martix[2][0] = 2;
            pc_move = true;
        }
        else if(place == 2 && board.martix[2][1] == 0 )
        {
            board.martix[2][1] = 2;
            pc_move = true;
        }
        else if(place == 3 && board.martix[2][2] == 0 )
        {
            board.martix[2][2] = 2;
            pc_move = true;
        }
        else if(place == 4 && board.martix[1][0] == 0 )
        {
            board.martix[1][0] = 2;
            pc_move = true;
        }
        else if(place == 5 && board.martix[1][1] == 0 )
        {
            board.martix[1][1] = 2;
            pc_move = true;
        }
        else if(place == 6 && board.martix[1][2] == 0 )
        {
            board.martix[1][2] = 2;
            pc_move = true;
        }
        else if(place == 7 && board.martix[0][0] == 0 )
        {
            board.martix[0][0] = 2;
            pc_move = true;
        }
        else if(place == 8 && board.martix[0][1] == 0 )
        {
            board.martix[0][1] = 2;
            pc_move = true;
        }
        else if(place == 9 && board.martix[0][2] == 0 )
        {
            board.martix[0][2] = 2;
            pc_move = true;
        }
        else
        {
            cout << "....make move properly...." << endl;
        }

        if(pc_move)
        {
            move_no += 1;

            system("cls");
            cout << "\t  Game Board";
            cout << endl << endl << endl;
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                {
                    cout << "    " ;
                    if(board.martix[i][j] == 1) cout << "O" ;
                    else if(board.martix[i][j] == 2) cout << "X" ;
                    else cout << " " ;
                    if(j!=2) cout << "    |";
                }
                if(i!=2) cout << "\n\n  -------------------------\n\n" ;
            }
            cout << endl << endl << endl;
            if(who_win(board,move_no) == 1)
            {
                cout << "\tCPU Win";
                break;
            }
            else if(who_win(board,move_no) == 2)
            {
                cout << "\tPlayer Win";
                break;
            }
            else if(who_win(board,move_no) == 0)
            {
                cout << "\tGame Draw";
                break;
            }
            movement m = choose_pc_move(board,move_no);
            board.martix[m.row][m.column] = 1;
            move_no += 1;
            Sleep(300);
            system("cls");
            cout << "\t  Game Board";
            cout << endl << endl << endl;
            for(int i=0;i<3;i++)
            {
                for(int j=0;j<3;j++)
                {
                    cout << "    " ;
                    if(board.martix[i][j] == 1) cout << "O" ;
                    else if(board.martix[i][j] == 2) cout << "X" ;
                    else cout << " ";
                    if(j!=2) cout << "    |";

                }
                if(i!=2) cout << "\n\n  -------------------------\n\n" ;
            }
            cout << endl << endl << endl;
            if(who_win(board,move_no) == 1)
            {
                cout << "\tCPU Win";
                break;
            }
            else if(who_win(board,move_no) == 2)
            {
                cout << "\tPlayer Win";
                break;
            }
            else if(who_win(board,move_no) == 0)
            {
                cout << "\tGame Draw";
                break;
            }
        }
    }
    cout << endl << endl << endl;
    string s;
    cout << "Do you want to paly again (Y/N)?  : ";
    cin >> s;
    if(s == "Y" || s == "y") goto redo;
    else
    {
        system("cls");
        thank_show();
    }
    return 0;
}

