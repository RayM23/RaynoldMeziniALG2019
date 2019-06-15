# RaynoldMeziniALG2019
package com.spiderman;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.HashSet;
import java.util.Scanner;

public class SpidermaniMeSyze {
    private static final int NiveliMax = 2;
    private HashSet<String> links;

    public WebCrawlerWithDepth() {
        links = new HashSet<>();
    }

    public void getPageLinks(String URL, int depth) throws IOException {
        if ((!links.contains(URL) && (depth < NiveliMax))) {
            System.out.println(">> Depth: " + depth + " [" + URL + "]");
            FileWriter omega = new FileWriter("DDr.txt", true);
            BufferedWriter bw = new BufferedWriter(omega);
            bw.write(URL);
            bw.newLine();
            bw.close();
            try {
                links.add(URL);

                Document document = Jsoup.connect(URL).get();
                Elements linksOnPage = document.select("a[href]");

                depth++;
                for (Element page : linksOnPage) {
                    getPageLinks(page.attr("abs:href"), depth);
                }
            } catch (IOException e) {
                System.err.println("For '" + URL + "': " + e.getMessage());
            }
        }
    }

    public static void main(String[] args) throws IOException {

        System.out.println("Fusni websitin qe doni te kontrolloni");
        Scanner sce = new Scanner(System.in);
        String buff = sce.nextLine();

        new SpidermaniMeSyze().getPageLinks(buff, 0);


    }
}
