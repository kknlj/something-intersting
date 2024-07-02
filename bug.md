# What's wrong with this code?

        import { useState } from "react";
        
        function App() {
        let id = 0;
        const INITIAL_TASKS = [
          { id: id++, label: 'Walk the dog' },
          { id: id++, label: 'Water the plants' },
          { id: id++, label: 'Wash the dishes' },
        ];
         return (
            <div>
              <h1>Todo List</h1>
              <div>
                <input type="text" placeholder="Add your task" onChange={(e) => setValue(e.target.value)} value={value} />
                <div>
                  <button 
                  onClick={() => {
                    if (value === "") return;
                    setList(
                      list.concat({
                        id: id++,
                        label: value.trim(),
                      }),
                    );
                    setValue('');
                  }}     
                  >Submit</button>
                </div>
              </div>
              <ul>
                {
                  list.map(
                    ({ id, label }) => (
                      <li key={id}>
                        <span>{label}</span>
                        <button onClick={
                          () => setList(list.filter((e) =>  {e.id != id}))
                        }>Delete</button>
                      </li>
                    )
                  )
                }
              </ul>
            </div>
          );
        }
        export default App;
**There are two errors in this code the first is that the id should be placed outside of the component to avoid initializing the value each time it is rendered causing elements to be added with all of their ids at 3. 
The second is this code**     
            
      setList(list.filter((e) => {e.id ! = id})) 
**should be written as**

      setList(list.filter((e) => e.id ! = id)) 
**. Because the above code doesn't return whether the result is true or not, the filter function filters all the elements.**😅 
