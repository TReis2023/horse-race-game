# Horse Race Game
This project uses Vue 3 as it's the modern version with better support with everything such as Pinia

## Horse Generation
While each horse gets a color the color word is also given for color blind support

## Race Logic
Condition overall gives a boost to the winrate but it's effect on the speed of the horses is lowered at the first and last 200 m of the race making the start and the end of the races and the shorter races overall more unpredictable

## Race
The races are split into tiles to show the change in speed towards the end and the beginning of the race more clearly. The first and last tile of the track are edge tiles where the horses have a speed that is determined more randomly compared to their speed at the middle tiles where its more determined by the condition stat of the horse.
