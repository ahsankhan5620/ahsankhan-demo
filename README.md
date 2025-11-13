# ahsankhan-demo
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

class Traffic {
public:
    string roadName;
    int vehicleCount;
    float avgSpeed;
    float density;
    int signalTime;

    void inputData() {
        cout << "\nEnter Road Name: ";
        cin >> roadName;
        cout << "Enter Vehicle Count per minute: ";
        cin >> vehicleCount;
        cout << "Enter Average Speed (km/h): ";
        cin >> avgSpeed;
        density = vehicleCount / avgSpeed;
        calculateSignalTime();
    }

    void calculateSignalTime() {
        if (density < 1)
            signalTime = 30; // Low traffic
        else if (density >= 1 && density < 3)
            signalTime = 45; // Medium traffic
        else
            signalTime = 60; // High traffic
    }

    void display() {
        cout << setw(15) << roadName
             << setw(15) << vehicleCount
             << setw(15) << avgSpeed
             << setw(15) << fixed << setprecision(2) << density
             << setw(15) << signalTime << " sec" << endl;
    }
};

int main() {
    int n;
    cout << "=== AI-Powered Traffic Flow Optimizer ===\n";
    cout << "Enter number of roads/intersections: ";
    cin >> n;

    Traffic road[50];

    for (int i = 0; i < n; i++) {
        cout << "\n--- Road " << i + 1 << " ---";
        road[i].inputData();
    }

    ofstream fout("traffic_report.txt");
    fout << "Road Name\tVehicle Count\tAverage Speed\tDensity\tSignal Time(sec)\n";

    cout << "\n\n=== Traffic Optimization Report ===\n";
    cout << setw(15) << "Road Name"
         << setw(15) << "Vehicles"
         << setw(15) << "Avg Speed"
         << setw(15) << "Density"
         << setw(15) << "Signal Time" << endl;

    for (int i = 0; i < n; i++) {
        road[i].display();
        fout << road[i].roadName << "\t"
             << road[i].vehicleCount << "\t"
             << road[i].avgSpeed << "\t"
             << road[i].density << "\t"
             << road[i].signalTime << endl;
    }

    fout.close();
    cout << "\nReport saved to 'traffic_report.txt'\n";
    cout << "\n--- End of Program ---";
    return 0;
}
