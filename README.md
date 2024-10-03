# WincrosoftPrevajalnik
Projekt za izziv prevajanje 
using System;
using System.IO;
using Google.Cloud.Translation.V2;

class TranslateReadme
{
    static void Main(string[] args)
    {
        // Pot do tvojega API ključa
        string apiKey = "YOUR_GOOGLE_TRANSLATE_API_KEY";

        // Ustvari Google Translate clienta
        var client = TranslationClient.CreateFromApiKey(apiKey);

        // Pot do README.md datoteke
        string filePath = "README.md";

        // Preberi vsebino README.md
        string readmeContent = File.ReadAllText(filePath);

        // Jeziki, v katere želiš prevesti
        string[] targetLanguages = { "sl", "de", "fr", "es" }; // npr. Slovenščina, Nemščina, Francoščina, Španščina

        foreach (var language in targetLanguages)
        {
            // Prevedi vsebino
            var translation = client.TranslateText(readmeContent, language);

            // Ustvari ime nove datoteke
            string translatedFilePath = $"README.{language}.md";

            // Shrani prevedeno vsebino v novo datoteko
            File.WriteAllText(translatedFilePath, translation.TranslatedText);

            Console.WriteLine($"Prevedeno v {language} in shranjeno v {translatedFilePath}");
        }

        Console.WriteLine("Prevajanje zaključeno.");
    }
}
