#!/bin/bash

# Print usage information
usage() {
    echo "Usage: $0 [-h] [-v] [-f FILE] [-o OUTPUT]"
    echo "Options:"
    echo "  -h          Show this help message and exit"
    echo "  -v          Enable verbose mode"
    echo "  -f FILE     Specify input file"
    echo "  -o OUTPUT   Specify output file"
    exit 1
}

# Initialize variables with default values
VERBOSE=false
INPUT_FILE=""
OUTPUT_FILE=""

# Parse command-line arguments
while getopts "hvf:o:" opt; do
    case $opt in
        h)
            usage
            ;;
        v)
            VERBOSE=true
            ;;
        f)
            INPUT_FILE="$OPTARG"
            ;;
        o)
            OUTPUT_FILE="$OPTARG"
            ;;
        \?)
            echo "Invalid option: -$OPTARG" >&2
            usage
            ;;
        :)
            echo "Option -$OPTARG requires an argument." >&2
            usage
            ;;
    esac
done

# Shift past the options to get positional arguments
shift $((OPTIND-1))

# Check for required arguments
if [ -z "$INPUT_FILE" ]; then
    echo "Error: Input file is required" >&2
    usage
fi

# Print parsed arguments (for debugging)
if [ "$VERBOSE" = true ]; then
    echo "Verbose mode: ON"
    echo "Input file: $INPUT_FILE"
    echo "Output file: $OUTPUT_FILE"
    echo "Positional arguments: $@"
fi

# Your script logic here
# Example:
# if [ -n "$OUTPUT_FILE" ]; then
#     echo "Processing $INPUT_FILE to $OUTPUT_FILE"
# else
#     echo "Processing $INPUT_FILE"
# fi




bashrc----------------------------------------------------------------------------------------------------------------------------------
# Manual JAVA_HOME switching function
setjdk() {
    if [ $# -ne 0 ]; then
        export JAVA_HOME=$(/usr/libexec/java_home -v $1)
        export PATH=$JAVA_HOME/bin:$PATH
        java -version
    else
        echo "Usage: setjdk <version> (e.g., setjdk 1.8, setjdk 11)"
    fi
}


