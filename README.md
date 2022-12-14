#include <iostream>
#include <vector>

using namespace std;

enum ClothingType
{
	SHIRT,
	JEANS,
	JACKET
};

class Clothing
{
private:
	string _name;
	string _description;
	string _location;
	string _color;
	int _size;
	ClothingType _type = SHIRT;
public:
	Clothing() {}

	Clothing(string name, string description, int size, string location, ClothingType type, string color) {
		_name = name;
		_description = description;
		_size = size;
		_location = location;
		_type = type;
		_color = color;
	}

	int GetSize() {
		return _size;
	}

	void SetSize(int value) {
		_size = value;
	}

	string GetName() {
		return _name;
	}

	ClothingType GetType() {
		return _type;
	}

	void ShowColor() {
		cout << "Color of this clothing is:" << _color << endl;
	}
};

class Wardrobe
{
public:
	Wardrobe() {};

	vector<Clothing> Clothings;

	void GoOut() {
		int count = 0;
		for (int i = 0; i < Clothings.size(); i++)
		{
			for (int j = 0; j < i; j++)
				if (Clothings[i].GetType() == Clothings[j].GetType())
					break;
				else
					count++;
		}	
		if (count < 3) {
			cout << "You are not ready to go!" << endl;
		}
		else
		{
			cout << "You are ready to go!" << endl;
		}
	}

	void SortBySize() {
		int temp;
		for (int i = 0; i < Clothings.size(); i++) {
			for (int j = i; j < Clothings.size(); j++)
			{
				if (Clothings[j].GetSize() < Clothings[i].GetSize()) {
					temp = Clothings[i].GetSize();
					Clothings[i].SetSize(Clothings[j].GetSize());
					Clothings[j].SetSize(temp);
				}
			}
		}

		for (int i = 0; i < Clothings.size(); i++) {
			cout << Clothings[i].GetName() << " - " << Clothings[i].GetSize() << endl;
		}
	}
};

int main()
{
	Clothing a ("Nike Jacket", "very good jacket", 33, "Lviv", ClothingType::JACKET, "Black");
	Clothing b ("Calvin Klein Jeans", "luxurious jeans", 28, "London", ClothingType::JEANS, "Brown");
	Clothing c("Tommy Shirt", "new model shirt", 18, "Ternopil", ClothingType::SHIRT, "Yellow");
	vector<Clothing> clothings1 = { a, b ,c };
	vector<Clothing> clothings2 = { b, c };

    Wardrobe wardrobe;
	cout << "First:" << endl;
	wardrobe.Clothings = clothings1;
	wardrobe.GoOut();

	for (int i = 0; i < wardrobe.Clothings.size(); i++) {
		wardrobe.Clothings[i].ShowColor();
	}
	cout << endl;

	wardrobe.SortBySize();
	cout << endl;

	wardrobe.Clothings = clothings2;
	wardrobe.GoOut();

	for (int i = 0; i < wardrobe.Clothings.size(); i++) {
		wardrobe.Clothings[i].ShowColor();
	}
	cout << endl;

	wardrobe.SortBySize();
    cout << endl;

	for (int i = 0; i < clothings1.size(); i++) {
		clothings1[i].ShowColor();
	}
}
