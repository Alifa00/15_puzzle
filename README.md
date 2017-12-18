```#include <cstdlib>
#include <iostream>
#include<sstream>
#include <array>
#include <utility>
#include <valarray>
using namespace std;

unsigned short fill_field(unsigned short* field);

void print_frame(unsigned short * arr);

bool move_h (unsigned short * field, unsigned short &position);

bool move_l (unsigned short * field, unsigned short &position);

bool move_k (unsigned short * field, unsigned short &position);

bool move_j (unsigned short * field, unsigned short &position);

bool win_check (unsigned short *field);

int main ()
{
  srand(time(nullptr));
  unsigned short field[16]={};//{1,2,3,4,5,6,7,8,9,10,11,12,13,14,15};
  unsigned short position =fill_field ( field);//= 15;
 
  for (;;)//j - сдвинуть вниз k - сдвинуть наверх h - сдвинуть влево l - сдвинуть вправо q - выйти
    {
      print_frame(field);
      char op;
      string input;
      getline (cin,input);
      istringstream str;
      str.str (input);
      if (!(str >> op) || str >> op)
        {
          	cout << "An error has occured while reading input data"<< endl;
                cin.get ();
		exit( EXIT_FAILURE);
                        
        }
      str.clear ();
      
      tolower (op);
      switch (op)
        {
        case 'h':
          {
            if (!(move_h (field,position)))
              {
                cout << "Can`t move to the left!\n ";
              }
             break;
          }
        case 'l':
          {
            if (!(move_l (field,position)))
              {
                cout << "Can`t move to the right!\n ";
              }
             break;
          }
        case 'k':
          {
            if (!(move_k (field,position)))
              {
                cout << "Can`t move up!\n ";
              }
             break;
          }
        case 'j':
          {
            if (!(move_j (field,position)))
              {
                cout << "Can`t move down!\n ";
              }
             break;
          }
        case'q':
          {
            cout << "exit";
            cin.get ();
            exit (0);
            break;
          }
        }        


      if (win_check (field))
        {
          cout << "You Won" << endl;
          print_frame (field);
          break;
        }
      

    
    }

  cout << endl << "Game Over \n Thank you for playing! ☺" << endl;
  cin.get ();
  return 0;
}

bool move_h (unsigned short * field, unsigned short & position)// число влево-> пустой вправо
{
  if (position%4 == 3 )
    {return false;}
  else 
    { swap( field[position],field[position +1]); position++; return true;}
}

bool move_l (unsigned short * field, unsigned short & position)// число вправо -> пустой влево
{
  if (position%4 == 0 )
    {return false;}
  else 
    { swap( field[position],field[position -1]); position--;return true;}
}

bool move_k (unsigned short * field, unsigned short & position)// число наверх -> пустой вниз
{
  if (position> 11 )
    {return false;}
  else 
    { swap( field[position],field[position +4]); position+=4; return true;}
}

bool move_j (unsigned short * field, unsigned short & position)// число вниз -> пустой наверх
{
  if (position< 4 )
    {return false;}
  else 
    { swap( field[position],field[position -4]); position-=4;return true;}
}
unsigned short fill_field(unsigned short* field)
{
	unsigned char numbers_used[15] = {};
        unsigned short buff;
	
		for (unsigned short i=0;i<15;i++)//((f_num | (unsigned short)(pow(2, (shift = rand() % 16)))) == f_num);
                  { 
                    while(!(field[i]) )
                      {
                        buff = rand() % 15 ;
                        if(!(numbers_used[buff]))
                          {
                             field[i]=  buff+1;
                             numbers_used[buff]=1; 
                             buff=0;     
                          }
                      }
                  }
            
        swap( field[buff=rand () % 15],field[15]);
        return buff;
}

bool win_check (unsigned short *field)
{
  for (unsigned int i=0;i<15;i++)
    {
      if( !(field[i]==i+1))return false;
    }
  return  true;
}

void print_frame(unsigned short * arr)//+
{
	
	
	for (unsigned char i = 0; i < 16; i++)
	{
		switch (i)
		{
		case 0:  {        cout << "  +----+----+----+----+" << endl  <<"  |"; break; }
		case 4:  {cout << endl << "  +----+----+----+----+" << endl  <<"  |" ; break; }
		case 8:  {cout << endl << "  +----+----+----+----+" << endl  <<"  |"; break; }
                case 12: {cout << endl << "  +----+----+----+----+" << endl  <<"  |"; break; }
               
                }
                
		switch (arr[i])
		{
		case 0: {cout << "    |"; break; }
		default : { cout <<" ";if (arr[i]<10) cout<< "0"; cout << arr[i] <<" |"; break; }
		
		}
	}
	cout << endl << "  +----+----+----+----+" << endl;
}
```
