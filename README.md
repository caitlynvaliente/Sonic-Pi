# Sonic-Pi
use_bpm 100

ch1  = [73, 68, 61]
ch2  = [76, 68, 61]
ch3  = [73, 68, 61]
ch4  = [73, 69, 54]
ch5  = [76, 69, 54]
ch6  = [73, 69, 54]
ch7  = [73, 69, 57]
ch8  = [76, 69, 57]
ch9  = [73, 69, 57]
ch10 = [75, 66, 59]
ch11 = [73, 66, 59]
ch12 = [71, 66, 59]

live_loop :shape do
  use_synth :beep
  with_synth_defaults amp: 0.2, sustain_level: 0.75, release: 0.5 do
    with_fx :reverb, room: 0.8 do
      with_fx :rlpf, cutoff: 100, res: 0.8 do
        play_pattern_timed [ch1, [], ch2, [], ch3, [],
                            ch4, [], ch5, [], ch6, [],
                            ch7, [], ch8, [], ch9, [],
        ch10, [], ch11, [], ch12, []],
          [0.25, 0.5, 0.25, 0.5, 0.25, 0.25]
      end
    end
  end
end

lch1 = [61, 64, 68]
lch2 = [66, 69, 73]
lch3 = [68, 71, 75]
lch4 = [73, 76, 80]

chs = [lch1, lch1, lch1, lch1, lch1, lch1,
       lch2, lch2, lch2, lch2, lch2, lch2,
       lch3, lch3, lch3, lch3, lch3, lch3,
       lch4, lch4, lch4, lch4, lch4, lch4].ring

tts = [0.25, 0.5, 0.25, 0.5, 0.25, 0.25].ring

cts = [50, 50, 60, 60, 70, 70, 80, 80,
       90, 90, 95, 96, 97, 100, 105, 110, 110, 105,
       100, 100, 90, 90, 80, 80, 70, 70, 60, 60].ring

live_loop :lead do
  use_synth :tech_saws
  with_synth_defaults amp: 2, sustain_level: 0.25, release: 0.95 do
    t = tick
    play chs[t], cutoff: (cts[t] / 1.1)
    sleep tts[t]
  end
end

samps = "path to samples"

live_loop :beat do
  4.times do
    sample samps, "bd", amp: 2
    sleep 0.75
    sample samps, "bd", amp: 2
    sleep 0.70
    sample samps, "clap", amp: 1.55
    sleep 0.05
    sample samps, "snare", amp: 1.45
    sleep 0.5
  end
end

live_loop :hihats do
  4.times do
    sleep 0.25
    sample samps, "hh", amp: 1
    sleep 0.25
    sample samps, "hh", amp: 2
  end
end

live_loop :hh2 do
  sleep 0.5
  4.times do
    sample samps, "hh", amp: 2
    sleep 0.125
  end
  sleep 3
end

live_loop :voices do
  sample samps, "oay", amp: 0.3
  sleep 6.5
  sample samps, "mhm", amp: 0.4
  sleep 1.5
end

