# README

a) Niveau facile

Quel est le nombre total d'objets Album contenus dans la base (sans regarder les id bien sûr) ?
  Album.all.length 
  ==> 347

Qui est l'auteur de la chanson "White Room" ?
  Track.where(title:"White Room").first.artist 
  ==> "Eric Clapton"

Quelle chanson dure exactement 188133 milliseconds ?
  Track.where(duration:"188133").first.title 
  ==> "Perfect"

Quel groupe a sorti l'album "Use Your Illusion II" ?
  Album.where(title:"Use Your Illusion II").first.artist 
  ==> "Guns N Roses"

b) Niveau Moyen

Combien y a t'il d'albums dont le titre contient "Great" ? (indice)
  Album.where("title like ?", "%Great%").length 
  ==> 13

Supprime tous les albums dont le nom contient "music".
  Album.where("title like ?", "%music%").destroy_all

Combien y a t'il d'albums écrits par AC/DC ?
  Album.where(artist: "AC/DC").length 
  ==> 2

Combien de chanson durent exactement 158589 millisecondes ?
  Track.where(duration: "158589").length
  ==> 0

c) Niveau Difficile
Pour ces questions, tu vas devoir effectuer des boucles dans la console Rails. C'est peu commun mais c'est faisable, tout comme dans IRB.

puts en console tous les titres de AC/DC.
  Track.where(artist: "AC/DC").each do |track|
    puts track.title
  end

puts en console tous les titres de l'album "Let There Be Rock".
  Track.where(album: "Let There Be Rock").each do |track|
   puts track.title
  end 

Calcule le prix total de cet album ainsi que sa durée totale.
  Track.where(album: "Let There Be Rock").reduce(0) do |sum, track|
    sum + track.price
  end.round(2)
  ==> 7.92
  Track.where(album: "Let There Be Rock").reduce(0) do |sum, track|
    sum + track.duration
  end.round(2)
  ==> 2453259

Calcule le coût de l'intégralité de la discographie de "Deep Purple".
  Track.where(artist: "Deep Purple").reduce(0) do |sum, track|
    sum + track.price
  end.round(2)
  ==> 90.09

Modifie (via une boucle) tous les titres de "Eric Clapton" afin qu'ils soient affichés avec "Britney Spears" en artist.
  Track.where(artist: "Eric Clapton").each do |track|
    track.update(artist: "Britney Spears")
  end 
