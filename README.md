from pathlib import Path

def analyze_file(file_path):
    try:
        text = file_path.read_text(encoding="utf-8")
        lines = text.splitlines()

        total = len(lines)
        empty = sum(1 for line in lines if not line.strip())
        content = total - empty
        longest = max((len(line) for line in lines), default=0)

        print(f"\nFile: {file_path.name}")
        print(f"Total lines: {total}")
        print(f"Content lines: {content}")
        print(f"Empty lines: {empty}")
        print(f"Longest line: {longest} characters")

    except Exception as error:
        print(f"Could not read {file_path.name}: {error}")

def main():
    folder = input("Enter folder path: ").strip()
    path = Path(folder)

    if not path.is_dir():
        print("Invalid folder path.")
        return

    files = list(path.glob("*.txt"))

    if not files:
        print("No text files found.")
        return

    for file in files:
        analyze_file(file)

if __name__ == "__main__":
    main()
