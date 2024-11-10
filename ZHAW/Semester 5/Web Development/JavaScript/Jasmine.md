#webdevelopment #sem5 #javascript 

- Testsuite besteht aus mehreren Specs
- Ziel in natürlicher Sprache beschrieben
- Suites und Specs sind Funktionen
- Für Node.js ebenso wie für Browser-Umgebung
![[Pasted image 20241021214331.png#invert]]
## Examples
```js
/* PlayerSpec.js - Auszug */
describe("when song has been paused", function() {
	beforeEach(function() {
		player.play(song) player.pause()
	})
	
	it("should indicate that the song is currently paused", function() {
		expect(player.isPlaying).toBeFalsy()
		
		/* demonstrates use of 'not' with a custom matcher */
		expect(player).not.toBePlaying(song)
	})
	
	it("should be possible to resume", function() {
		player.resume()
		expect(player.isPlaying).toBeTruthy()
		expect(player.currentlyPlayingSong).toEqual(song)
	})
})


expect([1, 2, 3]).toEqual([1, 2, 3]) expect(12).toBeTruthy() expect("").toBeFalsy() expect("Hello planet").not.toContain("world") expect(null).toBeNull() expect(8).toBeGreaterThan(5) expect(12.34).toBeCloseTo(12.3, 1) expect("horse_ebooks.jpg").toMatch(/\w+.(jpg|gif|png|svg)/i)
```