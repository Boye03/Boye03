
#include <iostream>
#include <string>
#include <vector>

struct Contact {
    std::string name;
    std::string phone_number;
};

void add_contact(std::vector<Contact>& phonebook) {
    std::string name, phone_number;
    std::cout << "Enter name: ";
    std::getline(std::cin, name);
    std::cout << "Enter phone number: ";
    std::getline(std::cin, phone_number);
    phonebook.push_back({name, phone_number});
    std::cout << "Contact added.\n";
}

void display_phonebook(const std::vector<Contact>& phonebook) {
    std::cout << "Phonebook:\n";
    for (const auto& contact : phonebook) {
        std::cout << contact.name << ": " << contact.phone_number << '\n';
    }
}

void search_phonebook(const std::vector<Contact>& phonebook, const std::string& name) {
    std::cout << "Search results for \"" << name << "\":\n";
    bool found = false;
    for (const auto& contact : phonebook) {
        if (contact.name == name) {
            std::cout << contact.name << ": " << contact.phone_number << '\n';
            found = true;
        }
    }
    if (!found) {
        std::cout << "No results found.\n";
    }
}

void update_contact(std::vector<Contact>& phonebook, const std::string& name) {
    bool found = false;
    for (auto& contact : phonebook) {
        if (contact.name == name) {
            std::string new_phone_number;
            std::cout << "Enter new phone number for " << name << ": ";
            std::getline(std::cin, new_phone_number);
            contact.phone_number = new_phone_number;
            found = true;
            std::cout << "Contact updated.\n";
        }
    }
    if (!found) {
        std::cout << "Contact not found.\n";
    }
}

void delete_contact(std::vector<Contact>& phonebook, const std::string& name) {
    auto it = phonebook.begin();
    while (it != phonebook.end()) {
        if (it->name == name) {
            it = phonebook.erase(it);
            std::cout << "Contact deleted.\n";
            return;
        } else {
            ++it;
        }
    }
    std::cout << "Contact not found.\n";
}

int main() {
    std::vector<Contact> phonebook;
    while (true) {
        std::cout << "Select an option:\n";
        std::cout << "1. Add contact\n";
        std::cout << "2. Display phonebook\n";
        std::cout << "3. Search phonebook\n";
        std::cout << "4. Update contact\n";
        std::cout << "5. Delete contact\n";
        std::cout << "6. Exit\n";
        std::cout << "> ";
        std::string choice_str;
        std::getline(std::cin, choice_str);
        if (choice_str.empty()) {
            continue;
        }
        char choice = choice_str[0];
        switch (choice) {
            case '1':
                add_contact(phonebook);
                break;
            case '2':
                display_phonebook(phonebook);
                break;
            case '3': {
                std::string name;
                std::cout << "Enter name to search: ";
                std::getline(std::cin, name);
                search_phonebook(phonebook, name);
                break;
            }
            case '4': {
                std::string name;
                std::cout << "Enter name to update: ";
                std::getline(std::cin, name);
                update_contact(phonebook, name);
                break;
            }
            case '5': {
                std::string name;
                std::cout << "Enter name to delete: ";
                std::getline(std::cin, name);
                delete_contact(phonebook, name);
                break;
            }
            case '6':
                std::cout << "Goodbye!\n";
                return 0;
            default:
                std::cout << "Invalid choice.\n";
                break;
        }
    }
}
