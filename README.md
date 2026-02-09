from nltk import tokenize
import nltk
import string

nltk.download("punkt")
nltk.download("stopwords")
nltk.download("wordnet")
nltk.download('punkt_tab')
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
from nltk.stem import WordNetLemmatizer

sentences = [
    "i am learning python and python",
    "we are happy today",
    "i am sad today"
]


def preprocess_text(documents):
  stop_words = stopwords.words("english")
  punctuations = string.punctuation
  cleaned_docyments = []

  for doc in documents:
    # step 1 : Lowercase
      raw_text = doc.lower()
      print ("After lowercase: ", raw_text)

            # step 2 : Tokenization
      tokens = word_tokenize(raw_text)
      print ("After tokenization: ", tokens)

      filtered_tokens = []
      for word in tokens:
        if word not in stop_words:
          filtered_tokens.append(word)
      print("Filteres Tokens :", filtered_tokens)

      clean_tokens = [word for word in filtered_tokens if word not in punctuations]
      print("Cleaned Tokens: ", clean_tokens)

      wnet = WordNetLemmatizer()

      lemmatized_words = []
      for word in clean_tokens:
        lemmatized_words.append(wnet.lemmatize(word, "v"))
        print("After lemmatization: ", lemmatized_words)


      final_tokens = []
      for word in lemmatized_words:
        if word.isalpha():
          final_tokens.append(word)
          print("Final tokens:", final_tokens)

      cleaned_text = " ".join(final_tokens)
      print("Cleaned Text: ", cleaned_text)



cleaned_sentences = preprocess_text(sentences)
print(cleaned_sentences)
