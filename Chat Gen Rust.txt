use std::io;
use rand::seq::SliceRandom;

fn main() {
    println!("Automated Chat Generator");

    loop {
        println!("Enter your message:");
        let mut input = String::new();
        io::stdin().read_line(&mut input).expect("Failed to read line");

        let response = generate_response(&input);
        println!("Bot: {}", response);
    }
}

fn generate_response(input: &str) -> String {
    // Responses based on keywords
    if input.contains("weather") {
        return "The weather is currently sunny and warm.".to_string();
    } else if input.contains("time") {
        let current_time = chrono::Local::now().format("%H:%M:%S");
        return format!("The current time is {}.", current_time);
    }

    // Responses based on patterns
    let greetings = vec!["Hello!", "Hi there!", "Hey!", "Greetings!"];
    let questions = vec!["How can I assist you?", "What can I do for you?", "Do you need any help?"];
    let responses = vec![
        "I'm sorry, I didn't quite understand that.",
        "Could you please rephrase that?",
        "Interesting. Tell me more.",
        "That's fascinating!",
    ];

    if input.contains("?") {
        return *questions.choose(&mut rand::thread_rng()).unwrap();
    } else if input.to_lowercase().contains("hello") || input.to_lowercase().contains("hi") {
        return *greetings.choose(&mut rand::thread_rng()).unwrap();
    } else {
        return *responses.choose(&mut rand::thread_rng()).unwrap();
    }
}
