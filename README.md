# vecHash
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
