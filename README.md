# vecHash
1. Given a list of integers, use a vector and return the median (when sorted, the value in the middle position) and mode (the value that occurs most often; a hash map will be helpful here) of the list.
```rust
use std::collections::HashMap;


fn analyze_lst(number: Vec<i32>) -> (f64, i32, i32) {
    let len = number.len();
    
    let sum: i32 = number.iter().sum();
    let mean: f64 = sum as f64/ len as f64;
    let test = len/2;
    println!("{test}");
    let mut sorted_number: Vec<i32> = number.clone();
    sorted_number.sort();
    let median: i32 = if len % 2 == 0 {
        (sorted_number[len/2-1] + sorted_number[len/2])/2
    } else {
        sorted_number[len/2]
    };

    let mut modd: HashMap<i32, i32> =HashMap::new();
    for &key in &number {
        *modd.entry(key).or_insert(0) += 1;
    }
    let mut best: (i32, i32) = {
        let first: (&i32, &i32) = modd.iter().next().expect("error"); // Берём первый элемент
        (*first.0, *first.1)
    };
    for (key, &value) in &modd {
        if value > best.1 {
            best = (*key, value);
        }
    }

    let mode = best.0;
    (mean, median, mode)
}


fn main() {
    let numbers = vec![5,5,3,3,5,2];
    let (mean, median, mode) = analyze_lst(numbers);
    println!("mean: {:.2}, median: {}, mode: {}", mean, median, mode);
}

```

3. Convert strings to pig latin. The first consonant of each word is moved to the end of the word and ay is added, so first becomes irst-fay. Words that start with a vowel have hay added to the end instead (apple becomes apple-hay). Keep in mind the details about UTF-8 encoding!
```rust
use std::collections::HashMap;
use std::string::String;

fn pig_latinas(text: &str) -> String {
    let flag: Vec<char> = vec!['a', 'e', 'i', 'o', 'u'];
    let mut words: Vec<String>= Vec::new();

    for i in text.split_whitespace() {
        //гласная
        let first = i.chars().next().unwrap_or_default();
        if flag.contains(&first.to_ascii_lowercase()) {
            words.push(format!("{}--hay", i)); 
        } else {
            // согласная
            let mut chars = i.chars();
            let first = chars.next().unwrap_or_default();
            let rest: String = chars.collect();
            words.push(format!("{}-{}ay", rest, first));
        }
    }
    words.join(" ")
}


fn main() {
    //aka--hay andom-ray unny-fay ext-tay
    let input_text = "aka random funny text";
    let output_text = pig_latinas(input_text);
    println!("{output_text}");
}

```
