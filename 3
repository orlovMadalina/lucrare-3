#include <iostream>
#include <vector>
#include <ctime>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <dirent.h>
#include <algorithm>

struct FileInfo {
    std::string name;
    std::string extension;
    std::time_t lastModifiedDateTime;
};

class FolderMonitor {
private:
    std::string folderPath;
    std::time_t lastSnapshotTime;
    std::vector<FileInfo> files;

public:
    FolderMonitor(const std::string& path) : folderPath(path), lastSnapshotTime(std::time(nullptr)) {}

    void updateSnapshot() {
        lastSnapshotTime = std::time(nullptr);
        scanFolder();
        std::cout << "Snapshot updated. Folder is now clean.\n";
    }

    void info(const std::string& fileName) {
        auto fileIt = std::find_if(files.begin(), files.end(),
            [&fileName](const FileInfo& file) { return file.name == fileName; });

        if (fileIt != files.end()) {
            printFileInfo(*fileIt);
        } else {
            std::cout << "File not found: " << fileName << "\n";
        }
    }

    void state() {
        std::cout << "Current Snapshot Time: " << std::asctime(std::localtime(&lastSnapshotTime));

        for (const auto& file : files) {
            std::cout << file.name << " - ";
            std::cout << (file.lastModifiedDateTime > lastSnapshotTime ? "Modified" : "Not modified") << "\n";
        }
    }

private:
    void scanFolder() {
        files.clear();
        DIR* dir;
        struct dirent* entry;

        if ((dir = opendir(folderPath.c_str())) != nullptr) {
            while ((entry = readdir(dir)) != nullptr) {
                std::string filePath = folderPath + "/" + entry->d_name;

                struct stat fileStat;
                if (stat(filePath.c_str(), &fileStat) == 0) {
                    if (S_ISREG(fileStat.st_mode)) {
                        FileInfo file;
                        file.name = entry->d_name;
                        file.extension = getFileExtension(file.name);
                        file.lastModifiedDateTime = fileStat.st_mtime;

                        // Additional logic for file type-specific information
                        // ...

                        files.push_back(file);
                    }
                }
            }
            closedir(dir);
        }
    }

    void printFileInfo(const FileInfo& file) {
        std::cout << "Name: " << file.name << "\n";
        std::cout << "Extension: " << file.extension << "\n";
        std::cout << "Last Modified Date Time: " << std::asctime(std::localtime(&file.lastModifiedDateTime));


        std::cout << "------------------------\n";
    }

    std::string getFileExtension(const std::string& fileName) {
        size_t dotPos = fileName.find_last_of(".");
        if (dotPos != std::string::npos) {
            return fileName.substr(dotPos + 1);
        }
        return "";
    }
};

int main() {
    FolderMonitor folderMonitor("/path/to/your/folder");

    std::string userInput;
    while (true) {
        std::cout << "Enter command: ";
        std::getline(std::cin, userInput);

        if (userInput == "update") {
            folderMonitor.updateSnapshot();
        } else if (userInput == "info") {
            std::string fileName;
            std::cout << "Enter file name: ";
            std::getline(std::cin, fileName);
            folderMonitor.info(fileName);
        } else if (userInput == "state") {
            folderMonitor.state();
        } else if (userInput == "exit") {
            break;
        } else {
            std::cout << "Invalid command. Try again.\n";
        }
    }

    return 0;
}
