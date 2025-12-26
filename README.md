import requests

def get_news(topic):
    api_key = "5c236e249e88413fa5ba1f6b473d09d2"
    url = f"https://newsapi.org/v2/everything?q={topic}&apiKey={api_key}&pageSize=5"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        articles = data['articles']
        if not articles:
            print(f"No news found for '{topic}'.")
            return
        print(f"\n📰 Top 5 news on '{topic}':")
        for i, article in enumerate(articles, 1):
            print(f"{i}. {article['title']} ({article['source']['name']})")
    else:
        print("Error fetching news.")


def get_covid_stats(country):
    url = f"https://disease.sh/v3/covid-19/countries/{country}"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print(f"\n COVID-19 Stats for {data['country']}:")
        print(f"Total Cases: {data['cases']}, Today's Cases: {data['todayCases']}")
        print(f"Deaths: {data['deaths']}, Today's Deaths: {data['todayDeaths']}")
        print(f"Recovered: {data['recovered']}, Active: {data['active']}")
    else:
        print(f"Could not fetch data for '{country}'.")




def get_word_meaning(word):
    url = f"https://api.dictionaryapi.dev/api/v2/entries/en/{word}"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        meanings = data[0]['meanings']
        print(f"\n📖 Meaning of '{word}':")
        for meaning in meanings:
            part_of_speech = meaning['partOfSpeech']
            defs = meaning['definitions']
            for d in defs:
                print(f"- ({part_of_speech}) {d['definition']}")
    else:
        print(f"No meaning found for '{word}'.")


def get_joke():
    url = "https://official-joke-api.appspot.com/jokes/random"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print(f"\n Joke:\n{data['setup']}\n{data['punchline']}")
    else:
        print("Error fetching joke.")



def ai_assistant():
    print(" Welcome to the Multi-API Student AI Assistant!")
    print("You can ask for: news, COVID stats, dictionary, joke.")
    print("Type 'exit' to quit.")

    while True:
        user_input = input("\nEnter your query: ").lower()
        if user_input == "exit":
            print("Goodbye! ")
            break



        if "news" in user_input:
            topic = input("Enter news topic: ")
            get_news(topic)
        elif "covid" in user_input:
            country = input("Enter country name: ")
            get_covid_stats(country)

        elif "dictionary" in user_input or "meaning" in user_input:
            word = input("Enter word to find meaning: ")
            get_word_meaning(word)
        elif "joke" in user_input:
            get_joke()
        else:
            print("I can fetch: news, COVID stats,dictionary, joke.")


ai_assistant()
