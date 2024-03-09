// ReportManagement
#include<iostream>
#include<fstream>
#include<string.h>
#include<conio.h>
using namespace std;

class StudentReport {
private:
    char studentName[100];
    char studentID[20];
    char subject[50];
    int marks;

public:
    void getStudentData();
    void displayStudentData();
    void addStudentRecord();
    void viewStudentRecords();
};

void StudentReport::getStudentData() {
    cout << "\nEnter Student Name: ";
    cin.getline(studentName, 100);
    cout << "Enter Student ID: ";
    cin.getline(studentID, 20);
    cout << "Enter Subject: ";
    cin.getline(subject, 50);
    cout << "Enter Marks: ";
    cin >> marks;
}

void StudentReport::displayStudentData() {
    cout << "\nStudent Name: " << studentName;
    cout << "\nStudent ID: " << studentID;
    cout << "\nSubject: " << subject;
    cout << "\nMarks: " << marks << endl;
}

void StudentReport::addStudentRecord() {
    ofstream outFile("student_records.txt", ios::app);
    if (!outFile) {
        cerr << "Error: Unable to open file." << endl;
        return;
    }
    getStudentData();
    outFile.write((char*)this, sizeof(*this));
    outFile.close();
    cout << "\nStudent Record Added Successfully!" << endl;
}

void StudentReport::viewStudentRecords() {
    ifstream inFile("student_records.txt");
    if (!inFile) {
        cerr << "Error: Unable to open file." << endl;
        return;
    }
    int count = 0;
    inFile.read((char*)this, sizeof(*this));
    while (!inFile.eof()) {
        count++;
        cout << "\nStudent Record " << count << ":" << endl;
        displayStudentData();
        inFile.read((char*)this, sizeof(*this));
    }
    inFile.close();
}

int main() {
    StudentReport obj;
    int choice;

    cout << "************ STUDENT REPORT MANAGEMENT SYSTEM ************" << endl;

    while (true) {
        cout << "\n1. Add Student Record\n";
        cout << "2. View Student Records\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                obj.addStudentRecord();
                break;
            case 2:
                obj.viewStudentRecords();
                break;
            case 3:
                cout << "\nExiting the program...\n";
                return 0;
            default:
                cout << "\nInvalid choice! Please enter a valid option.\n";
                break;
        }
    }

    return 0;
}

