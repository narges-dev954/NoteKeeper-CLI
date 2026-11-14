# NoteKeeper-CLI

while True:
    print("\n---- My Notebook ----")
    print("1. Add a note")
    print("2. Read notes")
    print("3. Delete a note")
    print("4. Edit a note")
    print("5. Search")
    print("6. Exit")

    choice = input("Choose an operation: ")

    # 1. Add a note
    if choice == "1":
        note = input("Write your note: ")

        with open("note.txt", "a") as file:
            file.write(note + "\n")

        print("Note saved!")

    # 2. Read notes
    elif choice == "2":
        try:
            with open("note.txt", "r") as file:
                notes = file.readlines()

            if notes:
                for i, note in enumerate(notes, start=1):
                    print(i, note.strip())
            else:
                print("Notebook is empty!")

        except FileNotFoundError:
            print("File not found!")

    # 3. Delete a note
    elif choice == "3":
        try:
            with open("note.txt", "r") as file:
                notes = file.readlines()

            if not notes:
                print("Notebook is empty!")
                continue

            for i, note in enumerate(notes, start=1):
                print(i, note.strip())

            number = int(input("Which note do you want to delete? "))

            if 1 <= number <= len(notes):
                deleted = notes.pop(number - 1)

                with open("note.txt", "w") as file:
                    file.writelines(notes)

                print("Deleted:", deleted.strip())
            else:
                print("Invalid note number!")

        except FileNotFoundError:
            print("File not found!")

        except ValueError:
            print("Please enter a valid number!")

    # 4. Edit a note
    elif choice == "4":
        try:
            with open("note.txt", "r") as file:
                notes = file.readlines()

            if not notes:
                print("Notebook is empty!")
                continue

            for i, note in enumerate(notes, start=1):
                print(i, note.strip())

            number = int(input("Which note do you want to edit? "))

            if 1 <= number <= len(notes):
                new_note = input("Write a new note: ")

                notes[number - 1] = new_note + "\n"

                with open("note.txt", "w") as file:
                    file.writelines(notes)

                print("Note updated!")
            else:
                print("Invalid note number!")

        except FileNotFoundError:
            print("File not found!")

        except ValueError:
            print("Please enter a valid number!")

    # 5. Search
    elif choice == "5":
        search_word = input("What do you want to search? ")

        try:
            with open("note.txt", "r") as file:
                notes = file.readlines()

            found = False

            for note in notes:
                if search_word in note:
                    print("Found:", note.strip())
                    found = True

            if not found:
                print("No note found!")

        except FileNotFoundError:
            print("File not found!")

    # 6. Exit
    elif choice == "6":
        print("Goodbye!")
        break

    else:
        print("Invalid choice!")
