#include <iostream>
#include <vector>
#include <string>

class MonitoredObject {
public:
    virtual void display() const = 0;
    virtual std::string getName() const = 0;
    virtual std::string getContent() const = 0;
    virtual void updateContent(const std::string& newContent) = 0;
};

class MonitoredDocument : public MonitoredObject {
private:
    std::string name;
    std::string content;
public:
    MonitoredDocument(const std::string& docName, const std::string& docContent) : name(docName), content(docContent) {}

    void display() const override {
        std::cout << "Document: " << name << std::endl;
        std::cout << "Content: " << content << std::endl;
    }

    std::string getName() const override {
        return name;
    }

    std::string getContent() const override {
        return content;
    }

    void updateContent(const std::string& newContent) override {
        content = newContent;
    }
};

class MonitorSystem {
private:
    std::vector<MonitoredObject*> monitoredObjects;
public:
    void addObject(MonitoredObject* obj) {
        monitoredObjects.push_back(obj);
    }

    void displayAll() const {
        for (const auto& obj : monitoredObjects) {
            obj->display();
        }
    }

    void detectChanges() {
        for (auto& obj : monitoredObjects) {
            std::cout << "Checking for changes in " << obj->getName() << std::endl;
            std::string currentContent = obj->getContent();
            if (currentContent != obj->getContent()) {
                std::cout << "Changes detected!" << std::endl;
            } else {
                std::cout << "No changes detected." << std::endl;
            }
        }
    }

    void commitChanges(const std::string& message) const {
        std::cout << "Committing changes with message: " << message << std::endl;

    }
};

int main() {
    MonitoredDocument document1("document1.txt", "Initial content");
    MonitoredDocument document2("document2.txt", "Initial content");

    MonitorSystem monitorSystem;
    monitorSystem.addObject(&document1);
    monitorSystem.addObject(&document2);

    std::cout << "Lista de obiecte monitorizate:" << std::endl;
    monitorSystem.displayAll();

    std::cout << "\nDetectarea modificărilor:" << std::endl;
    monitorSystem.detectChanges();

    document1.updateContent("New content for document1");

    std::cout << "\nDetectarea modificărilor după actualizare:" << std::endl;
    monitorSystem.detectChanges();

    monitorSystem.commitChanges("Adăugat funcționalitate de monitorizare și detectare");

    return 0;
}
