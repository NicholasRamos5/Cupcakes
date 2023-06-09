<head>
<meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <script src="https://kit.fontawesome.com/b33dd8950a.js" crossorigin="anonymous"></script>
  <title>Editor</title>
  <style type="text/css" media="screen">

	::-webkit-scrollbar {
	width: 8px;
	}

	/* Track */
	::-webkit-scrollbar-track {
	background: #141414;
	}

	/* Handle */
	::-webkit-scrollbar-thumb {
	background: #4a4a4a;
	border-radius: 4px;
	}

	/* Handle on hover */
	::-webkit-scrollbar-thumb:hover {
	background: #323232;
	}

    #editor {
        margin: 0;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
		width: 80vw;
		height: 500px;
		font-size: 14px;
		border-radius: 10px;
		resize: vertical;
		overflow-x: auto;
    }

	#outputBox {
		margin: 0;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		width: 80vw;
		text-align: left;
		font-size: 16px;
		border-radius: 10px;
	}

	button {
		background-color: white;
		border: none;
		color: black;
		padding: 15px 32px;
		width: 80%;
		text-align: center;
		text-decoration: none;
		display: inline-block;
		font-size: 16px;
		margin: 4px 2px;
		border-radius: 10px;
		cursor: pointer;
		transition: all 0.2s ease-in-out;
	}

	button:hover {
		background-color: #808080;
		color: white;
		transform: translateY(-2px);
	}

	h1 {
		text-align: center;
	}

	select {
		width: 80%;
		padding: 16px 20px;
		margin: 16px;
		border: none;
		border-radius: 4px;
		background-color: #232323;
		color: white;
	}
  </style>
</head>

<h1> Code Editor </h1>

<form>
	<center>
	<select id="preset-select">
		<option value="">Select a preset</option>
		<option value="merge-sort">Merge Sort</option>
		<option value="hello-world">Hello World</option>
	</select>
	<div id="editor">public class Main {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}</div>
    <!-- <textarea id="code" style="width: 500px; height: 500px;"></textarea> -->
    <br/>
    <button id="runButton" type="button">Run Code</button>
    </center>
</form>
<br/>
<center>
<pre id="outputBox">Code Output Here</pre>
</center>

<!-- https://github.com/ajaxorg/ace-builds/blob/master/src-noconflict/ace.js -->
<script src="https://cdn.jsdelivr.net/npm/ace-builds@1.4.13/src-min/ace.js"></script>
<script>
    var editor = ace.edit("editor");
    editor.setTheme("ace/theme/twilight");
    editor.session.setMode("ace/mode/java");
	ace.require("ace/ext/language_tools");
    <!-- // enable autocompletion and snippets -->
    editor.setOptions({
        enableBasicAutocompletion: true,
        enableSnippets: true,
        enableLiveAutocompletion: false
    });
</script>

<script>
  const select = document.getElementById('preset-select');
  document.getElementById('editor').addEventListener("mouseup", function() {
	resizableElement.style.height = resizableElement.clientHeight + "px";
	});

  select.addEventListener('change', function() {
    // Get the selected option value
    const selectedPreset = select.value;

    // Update the editor content based on the selected preset
    if (selectedPreset === 'merge-sort') {
      editor.setValue(`class Main {
    // Merges two subarrays of arr[].
    // First subarray is arr[l..m]
    // Second subarray is arr[m+1..r]
    void merge(int arr[], int l, int m, int r)
    {
        // Find the sizes of two subarrays to be merged
        int n1 = m - l + 1;
        int n2 = r - m;

        /* Create temp arrays */
        int[] L = new int[n1];
        int[] R = new int[n2];
 
        /* Copy data to temp arrays */
        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];

        /* Merge the temp arrays */

        // Initial indexes of first and second subarrays
        int i = 0, j = 0;

        // Initial index of merged subarray array
        int k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                // MISSING CODE #1
            }
            else {
                // MISSING CODE #2
            }
            k++;
        }

        /* Copy remaining elements of L[] if any */
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy remaining elements of R[] if any */
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    // Main function that sorts arr[l..r] using
    // merge()
    void sort(int[] arr, int l, int r)
    {
        if (l < r) {
            // COMMENT A
            int m = l + (r - l) / 2;

            // COMMENT B
            sort(arr, l, m);
            sort(arr, m + 1, r);

            // COMMENT C
            merge(arr, l, m, r);
        }
    }

    /* A utility function to print array of size n */
    static void printArray(int[] arr)
    {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        int[] arr = { 12, 11, 13, 5, 6, 7 };
 
        System.out.println("Given Array");
        printArray(arr);

        Main ob = new Main();
        ob.sort(arr, 0, arr.length - 1);

        System.out.println("\\nSorted array");
        printArray(arr);
    }
}`);
    } else if (selectedPreset === 'hello-world') {
      editor.setValue(`public class Main {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}`)
    } else {
      // If no preset is selected, reset the editor content
      editor.textContent = 'public class Main {\n  public static void main(String[] args) {\n    System.out.println("Hello World!");\n  }\n}';
    }
  });
</script>


<script>
 const button = document.querySelector('#runButton');
 const outputBox = document.getElementById("outputBox");
 function runCode() {
  const API_URL = 'https://csaq.aadit.dev/j0/run/';
  var code = editor.getValue();
  // encode code variable to base64
  code2 = btoa(code);
  console.log(code2);

  button.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Running Code...';
  button.disabled = true;

  const headers = {
   'content-type': 'application/json'
  };

  const data = {
   code: code2,
  };

  fetch(API_URL, {
   method: 'POST',
   headers: headers,
   mode: 'cors',
   cache: 'no-cache',
   body: JSON.stringify(data),
  })
   .then((response) => response.text())
   .then((data) => {
    outputBox.style.color = 'white';
	console.log('Output: ' + data);
	outputBox.innerHTML = data;
	button.innerHTML = 'Run Code';
	button.disabled = false;
   })
   .catch((error) => {
    console.error(error);
    outputBox.style.color = 'red';
    outputBox.innerHTML = error;
    button.innerHTML = 'Submit';
    button.disabled = false;
   });
 }

 button.addEventListener('click', runCode);
</script>


<!-- 
MISSING CODE 1
arr[k] = L[i];
i++;

MISSING CODE 2
arr[k] = R[j];
j++;
-->
