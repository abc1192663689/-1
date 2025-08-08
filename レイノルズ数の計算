#include <iostream>
#include <cmath>
#include <limits>
#include <map>
#include <string>

using namespace std;


class pipe {
public:
    pipe() {}
    string name;
    double D = 0; // 代表長さ
    pipe(const string& n, double d) : name(n), D(d) {}
};

class shapeselection {
private:
    map<int, pipe> duct;
public:
    shapeselection() {
        duct[1] = pipe("円管", 0.0);
        duct[2] = pipe("環状隙間", 0.0);
        duct[3] = pipe("長方形", 0.0);
        duct[4] = pipe("正方形", 0.0);
        duct[5] = pipe("任意代表長さ", 0.0);
        duct[6] = pipe("平板", 0.0);
    }

    template<typename T>
    T input(const string& prompt) {
        T v{};
        while (true) {
            cout << prompt;
            if (!(cin >> v)) {
                cout << "数値を入れてください。\n";
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
            }
            else {
                return v;
            }
        }
    }

    void theSHAPeofpipe() {
        cout << "-- 管形状選択 --\n";
        for (auto it = duct.begin(); it != duct.end(); ++it) {
            cout << " " << it->first << ") " << it->second.name << "\n";
        }
        int choice = input<int>("選択番号: ");
        if (duct.find(choice) == duct.end()) {
            cout << "無効な選択。\n";
            exit(1);
        }

        switch (choice) {
        case 1: {
            double Di = input<double>("円管内径 Di [m]: ");
            duct[choice].D = Di;
            break;
            int p = 1;
        }
        case 2: {
            double Do = input<double>("外径 Do [m]: ");
            double Di = input<double>("内径 Di [m]: ");
            duct[choice].D = Do - Di;
            break;
            int p = 2;
        }
        case 3: {
            double a = input<double>("幅 a [m]: ");
            double b = input<double>("高さ b [m]: ");
            duct[choice].D = 4.0 * (a * b) / (2.0 * (a + b));
            break;
            int p = 3;
        }
        case 4: {
            double a = input<double>("辺の長 a [m]: ");
            duct[choice].D = a;
            break;
            int p = 4;
        }
        case 5: {
            duct[choice].D = input<double>("代表長さ D [m]: ");
            break;
            int p = 5;
        }
        case 6: {
            duct[choice].D = input<double>("流れる長さL [m]: ");
            break;
            int p = 6;
        }
        }
    }

    void calculate() {
        int p = 0;
        double D = 0.0;
        for (auto it = duct.begin(); it != duct.end(); ++it) {
            if (it->second.D > 0.0) D = it->second.D;
        }
        if (D <= 0) {
            cout << "代表長さが設定されていない。\n";
            exit(1);
        }
        cout << "\n入力方法選択:\n1) 平均流速Vと動粘度ν入力\n2) 平均流速と粘度η,密度ρ入力\n";
        int method = input<int>("方法番号: ");
        double V = 0.0, ν = 0.0;
        if (method == 1) {
            V = input<double>("平均流速 V [m/s]: ");
            ν = input<double>("動粘度 ν [m^2/s]: ");
        }
        else if (method == 2) {
            V = input<double>("平均流速 V [m/s]: ");
            double μ = input<double>("粘度μ[Pa·s]: ");
            double ρ = input<double>("密度ρ[kg/m^3]: ");
            ν = μ / ρ;
        }

        double Re = V * D / ν;

        {
            cout << "\n--- 結果 ---\n";
            cout << "D = " << D << " m, V = " << V << " m/s, Re=" <<Re<< "\n";


            if ((int)p == 6) {

                if (Re < 530000)
                    cout << "層流\n";
                else
                    cout << "乱流\n";
            }

            else {
                if (Re < 2300) {
                    cout << "層流\n";
                }
                else if
                    (Re <= 4000) cout << "遷移領域\n";
                else cout << "乱流\n";
            }
        };
    };
};

int main() {
    shapeselection rc;
    rc.theSHAPeofpipe();
    rc.calculate();
    return 0;
}
