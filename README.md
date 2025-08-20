#!/usr/bin/env python3
"""
JSON Pretty Printer
- Reads a JSON file given as argument
- Writes a human-readable pretty-printed version
"""

import json, sys, pathlib

def main():
    if len(sys.argv) < 2:
        print("Usage: python3 pretty.py <file.json>")
        sys.exit(1)

    path = pathlib.Path(sys.argv[1])
    if not path.exists():
        print(f"File not found: {path}")
        sys.exit(1)

    try:
        data = json.loads(path.read_text(encoding="utf-8"))
    except Exception as e:
        print(f"Invalid JSON: {e}")
        sys.exit(1)

    out_path = path.with_name(path.stem + "_pretty.json")
    out_path.write_text(json.dumps(data, indent=2, ensure_ascii=False), encoding="utf-8")

    print(f"Pretty JSON written to {out_path}")

if __name__ == "__main__":
    main()
