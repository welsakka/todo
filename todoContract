pragma solidity ^0.4.20;

contract TodoList {
    
    struct Note {
        uint id;
        bytes32 note;
        uint256 date;
        address owner;
        bool isCompleted;
    }
    
    //constant variable to minimize gas used
    uint public constant maxAmountOfTodos = 100;
    
    //Each address is assigned a max of 100 notes
    //Note[maxAmountOfTodos] is an array of Note structs
    mapping(address => Note[maxAmountOfTodos]) public todos;
    
    //assigns an unsigned integer to every possible address; used to track
    //specific note created by a single address
    mapping(address => uint) public lastID;
    
    modifier onlyOwner(address _owner) {
        require(msg.sender == _owner);
        _;
    }
    
    //Function to add a note
    function addNote(bytes32 _content) public{
        //single note created called myNote of struct type Note
        Note memory myNote = Note(lastID[msg.sender], _content, now, msg.sender, false);
        //single note added to mapping, associated with address of msg.sender
        todos[msg.sender][lastID[msg.sender]] = myNote;
        if (lastID[msg.sender] >= maxAmountOfTodos)
            lastID[msg.sender] = 0;
        else
            lastID[msg.sender]++;
    }
    
    //uint _noteID is the specific note the user wants access to in the Note array
    function markNoteAsComplete(uint _noteID) public onlyOwner(todos[msg.sender][_noteID].owner) {
        //noteID must be less than 100
        require(_noteID < maxAmountOfTodos);
        //Note must be marked as incomplete
        require(!todos[msg.sender][_noteID].isCompleted);
        todos[msg.sender][_noteID].isCompleted = true;
    }
    
    
}
