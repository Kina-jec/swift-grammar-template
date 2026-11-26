#生成AIに聞いたこと

import SwiftUI

struct RankingView: View {

    // 保存されているスコアを入れる配列

    @State private var scores: [Int] = []

    var body: some View {

        ZStack {

            // 背景画像

            Image("halloweenBackground")

                .resizable()

                .scaledToFill()

                .ignoresSafeArea()

            // 背景を少し暗くして文字を見やすくする

            Color.black

                .opacity(0.3)

                .ignoresSafeArea()

            VStack(spacing: 20) {

                // タイトル

                Text("スコアランキング")

                    .font(.largeTitle)

                    .bold()

                // ベストスコア

                Text("BEST SCORE")

                    .foregroundStyle(.yellow)

                    .bold()

                Text("\(scores.max() ?? 0)")

                    .font(.system(size: 50, weight: .bold))

                    .foregroundStyle(.yellow)

                // ランキング

                VStack(spacing: 5) {

                    ForEach(

                        Array(scores.sorted(by: >).prefix(5).enumerated()),

                        id: \.offset

                    ) { index, score in

                        HStack {

                            // メダル

                            Text(rankMark(index))

                            // 順位

                            Text("\(index + 1)位")

                                .bold()

                            Spacer()

                            // スコア

                            Text("\(score) 点")

                                .bold()

                        }

                        .font(.title3)

                        .padding()

                    }

                    // まだスコアがない場合

                    if scores.isEmpty {

                        Text("まだスコアがありません")

                            .padding()

                    }

                }

                .background(

                    Color.black.opacity(0.5)

                )

                .clipShape(

                    RoundedRectangle(cornerRadius: 20)

                )

                .padding(.horizontal)

                Spacer()

                // ホームボタン

                Button("⌂ ホーム") {

                    // ホーム画面へ戻る処理

                }

                .buttonStyle(.borderedProminent)

                .padding(.bottom, 30)

            }

            .padding(.top, 30)

            .foregroundStyle(.white)

        }

        // RankingViewが表示されたときに

        // 保存済みスコアを読み込む

        .onAppear {

            loadScores()

        }

    }

    // MARK: - スコア読み込み

    func loadScores() {

        scores = UserDefaults.standard.array(

            forKey: "scoreHistory"

        ) as? [Int] ?? []

    }

    // MARK: - 順位マーク

    func rankMark(_ index: Int) -> String {

        if index == 0 {

            return "1"

        } else if index == 1 {

            return "2"

        } else if index == 2 {

            return "3"

        } else {

            return "ランク外"

        }

    }

}

#Preview {

    RankingView()

}

スコアランキングやbest score ,スコア の文字をハロウィンの世界観で、みやすく、可愛くしてください


#回答

import SwiftUI

struct RankingView: View {

    // 保存されているスコアを入れる配列
    @State private var scores: [Int] = []

    var body: some View {

        ZStack {

            // 背景画像
            Image("halloweenBackground")
                .resizable()
                .scaledToFill()
                .ignoresSafeArea()

            // 背景を少し暗くする
            Color.black
                .opacity(0.35)
                .ignoresSafeArea()

            VStack(spacing: 18) {

                // =========================
                // タイトル
                // =========================

                Text("🎃 SCORE RANKING 🎃")
                    .font(.system(size: 32, weight: .black))
                    .foregroundStyle(.orange)
                    .shadow(color: .black, radius: 3, x: 2, y: 2)

                Text("スコアランキング")
                    .font(.title2)
                    .bold()
                    .foregroundStyle(.white)
                    .shadow(color: .purple, radius: 5)


                // =========================
                // ベストスコア
                // =========================

                VStack(spacing: 5) {

                    Text("👑 BEST SCORE 👑")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.yellow)

                    Text("\(scores.max() ?? 0)")
                        .font(.system(size: 55, weight: .black))
                        .foregroundStyle(.yellow)
                        .shadow(
                            color: .orange,
                            radius: 8
                        )

                    Text("POINTS")
                        .font(.caption)
                        .bold()
                        .foregroundStyle(.white.opacity(0.8))
                }
                .padding(.vertical, 12)
                .padding(.horizontal, 35)
                .background(
                    Color.purple.opacity(0.55)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 20)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 20)
                        .stroke(
                            Color.orange,
                            lineWidth: 2
                        )
                )


                // =========================
                // ランキング
                // =========================

                VStack(spacing: 8) {

                    ForEach(
                        Array(
                            scores
                                .sorted(by: >)
                                .prefix(5)
                                .enumerated()
                        ),
                        id: \.offset
                    ) { index, score in

                        HStack(spacing: 12) {

                            // メダル
                            Text(rankMark(index))
                                .font(.title)

                            // 順位
                            Text("\(index + 1)位")
                                .font(.headline)
                                .bold()
                                .foregroundStyle(rankColor(index))

                            Spacer()

                            // スコア
                            Text("\(score) 点")
                                .font(.title3)
                                .bold()
                                .foregroundStyle(.white)
                        }
                        .padding()
                        .background(
                            Color.black.opacity(0.45)
                        )
                        .clipShape(
                            RoundedRectangle(cornerRadius: 15)
                        )
                    }


                    // スコアがない場合
                    if scores.isEmpty {

                        VStack(spacing: 10) {

                            Text("👻")
                                .font(.system(size: 40))

                            Text("まだスコアがありません")
                                .bold()
                                .foregroundStyle(.white)

                            Text("ゲームを遊んでスコアを残そう！")
                                .font(.caption)
                                .foregroundStyle(.white.opacity(0.8))
                        }
                        .padding()
                    }
                }
                .padding()
                .background(
                    Color.black.opacity(0.55)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 25)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 25)
                        .stroke(
                            Color.purple.opacity(0.8),
                            lineWidth: 2
                        )
                )
                .padding(.horizontal, 20)


                Spacer()


                // =========================
                // ホームボタン
                // =========================

                Button {
                    // ホーム画面へ戻る処理
                } label: {

                    Text("🏠 ホームへ戻る")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.white)
                        .padding(.horizontal, 30)
                        .padding(.vertical, 12)
                        .background(
                            Color.orange
                        )
                        .clipShape(
                            Capsule()
                        )
                        .shadow(
                            color: .black.opacity(0.5),
                            radius: 5
                        )
                }
                .padding(.bottom, 30)
            }
            .padding(.top, 30)
        }

        // RankingViewが表示されたとき
        .onAppear {
            loadScores()
        }
    }


    // MARK: - スコア読み込み

    func loadScores() {

        scores = UserDefaults.standard.array(
            forKey: "scoreHistory"
        ) as? [Int] ?? []
    }


    // MARK: - 順位マーク

    func rankMark(_ index: Int) -> String {

        if index == 0 {
            return "🥇"
        } else if index == 1 {
            return "🥈"
        } else if index == 2 {
            return "🥉"
        } else if index == 3 {
            return "🎃"
        } else {
            return "👻"
        }
    }


    // MARK: - 順位の色

    func rankColor(_ index: Int) -> Color {

        if index == 0 {
            return .yellow
        } else if index == 1 {
            return .white
        } else if index == 2 {
            return .orange
        } else {
            return .white
        }
    }
}


#Preview {
    RankingView()
}


#AIに聞いたこと
絵文字を使うのではなく、背景色を使い、可愛く、もっとみやすく変えてください


#回答
import SwiftUI

struct RankingView: View {

    @State private var scores: [Int] = []

    var body: some View {

        ZStack {

            // 背景画像
            Image("halloweenBackground")
                .resizable()
                .scaledToFill()
                .ignoresSafeArea()

            // 背景を暗くして文字を読みやすくする
            Color.black
                .opacity(0.35)
                .ignoresSafeArea()

            VStack(spacing: 20) {

                // =========================
                // タイトル
                // =========================

                Text("SCORE RANKING")
                    .font(.system(size: 32, weight: .black))
                    .foregroundStyle(.white)
                    .padding(.horizontal, 30)
                    .padding(.vertical, 12)
                    .background(
                        Color.purple.opacity(0.85)
                    )
                    .clipShape(
                        RoundedRectangle(cornerRadius: 20)
                    )
                    .overlay(
                        RoundedRectangle(cornerRadius: 20)
                            .stroke(Color.orange, lineWidth: 3)
                    )
                    .shadow(
                        color: .black.opacity(0.4),
                        radius: 5,
                        y: 3
                    )


                // =========================
                // BEST SCORE
                // =========================

                VStack(spacing: 5) {

                    Text("BEST SCORE")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.purple)

                    Text("\(scores.max() ?? 0)")
                        .font(.system(size: 50, weight: .black))
                        .foregroundStyle(.orange)

                    Text("POINTS")
                        .font(.caption)
                        .bold()
                        .foregroundStyle(.purple.opacity(0.7))
                }
                .frame(maxWidth: .infinity)
                .padding(.vertical, 15)
                .background(
                    Color(red: 1.0, green: 0.92, blue: 0.72)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 22)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 22)
                        .stroke(Color.orange, lineWidth: 3)
                )
                .shadow(
                    color: .black.opacity(0.3),
                    radius: 5,
                    y: 3
                )
                .padding(.horizontal, 25)


                // =========================
                // ランキング
                // =========================

                VStack(spacing: 10) {

                    ForEach(
                        Array(
                            scores
                                .sorted(by: >)
                                .prefix(5)
                                .enumerated()
                        ),
                        id: \.offset
                    ) { index, score in

                        HStack {

                            // 順位
                            Text("\(index + 1)")
                                .font(.title2)
                                .bold()
                                .foregroundStyle(.white)
                                .frame(width: 45, height: 45)
                                .background(
                                    rankColor(index)
                                )
                                .clipShape(Circle())

                            Text("\(index + 1)位")
                                .font(.headline)
                                .bold()
                                .foregroundStyle(.white)

                            Spacer()

                            // スコア
                            Text("\(score)")
                                .font(.title2)
                                .bold()
                                .foregroundStyle(.yellow)

                            Text("点")
                                .font(.subheadline)
                                .foregroundStyle(.white)
                        }
                        .padding(.horizontal, 15)
                        .padding(.vertical, 10)
                        .background(
                            Color.purple.opacity(0.75)
                        )
                        .clipShape(
                            RoundedRectangle(cornerRadius: 18)
                        )
                        .overlay(
                            RoundedRectangle(cornerRadius: 18)
                                .stroke(
                                    index == 0
                                        ? Color.orange
                                        : Color.white.opacity(0.25),
                                    lineWidth: index == 0 ? 3 : 1
                                )
                        )
                    }


                    // スコアがない場合
                    if scores.isEmpty {

                        Text("まだスコアがありません")
                            .font(.headline)
                            .foregroundStyle(.white)
                            .frame(maxWidth: .infinity)
                            .padding(.vertical, 30)
                    }
                }
                .padding(15)
                .background(
                    Color.black.opacity(0.6)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 25)
                )
                .padding(.horizontal, 20)


                Spacer()


                // =========================
                // ホームボタン
                // =========================

                Button {

                    // ホーム画面へ戻る処理

                } label: {

                    Text("ホームへ戻る")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.white)
                        .frame(width: 180)
                        .padding(.vertical, 13)
                        .background(
                            Color.orange
                        )
                        .clipShape(
                            RoundedRectangle(cornerRadius: 18)
                        )
                        .shadow(
                            color: .black.opacity(0.4),
                            radius: 4,
                            y: 3
                        )
                }
                .padding(.bottom, 30)
            }
            .padding(.top, 30)
        }
        .onAppear {
            loadScores()
        }
    }


    // MARK: - スコア読み込み

    func loadScores() {

        scores = UserDefaults.standard.array(
            forKey: "scoreHistory"
        ) as? [Int] ?? []
    }


    // MARK: - 順位ごとの色

    func rankColor(_ index: Int) -> Color {

        if index == 0 {

            // 1位
            return Color.orange

        } else if index == 1 {

            // 2位
            return Color.purple.opacity(0.8)

        } else if index == 2 {

            // 3位
            return Color.brown.opacity(0.8)

        } else {

            // 4位・5位
            return Color.gray.opacity(0.7)
        }
    }
}


#Preview {
    RankingView()
}

#AIに聞いたこと
このコードはエラーが出ています

#回答
（すみません。前のコードは少し複雑にしすぎました。

どのエラーかを正確に直したいので、Xcodeに出ている赤いエラーメッセージをそのまま送ってください。
スクリーンショットでも大丈夫です。

特に、赤線が付いている場所が分かるとすぐ特定できます。

なお、前のコードでまず確認してほしいのは rankColor の部分です。より単純に、次のように書き換えてください。）
func rankColor(_ index: Int) -> Color {
    if index == 0 {
        return .orange
    } else if index == 1 {
        return .purple
    } else if index == 2 {
        return .brown
    } else {
        return .gray
    }
}
（また、この部分も環境によって分かりにくいので、）
.stroke(
    index == 0
        ? Color.orange
        : Color.white.opacity(0.25),
    lineWidth: index == 0 ? 3 : 1
)
（いったん簡単にして、）
.stroke(Color.orange, lineWidth: 2)
（にしてみてください。

つまり、）
.overlay(
    RoundedRectangle(cornerRadius: 18)
        .stroke(Color.orange, lineWidth: 2)
)
でOKです。

エラーメッセージか、エラーが出ているXcode画面を送ってもらえれば、今の RankingView を丸ごとエラーが出ない形に直します。

#AIに聞いてみた
The compiler is unable to type-check this expression in reasonable time; try breaking up the expression into distinct sub-expressions と言うエラーが7行目に出てきました

#回答
（はい、このエラーなら原因がかなり分かります。

The compiler is unable to type-check this expression in reasonable time...

これは文法が間違っているというより、body の中が複雑になりすぎて、Swiftコンパイラが型を判断するのに時間がかかりすぎているときによく出ます。

7行目が var body: some View { なら、7行目そのものが悪いとは限りません。その中に書かれているSwiftUIの処理全体が複雑なのが原因です。

今回の場合、特にこの部分が複雑です。）
ForEach(
    Array(
        scores
            .sorted(by: >)
            .prefix(5)
            .enumerated()
    ),
    id: \.offset
) { index, score in

（まず、ランキング用データを別の変数に分離しましょう。これが一番簡単です。

修正版

body より上に、これを追加してください。）

var rankingScores: [Int] {
    Array(scores.sorted(by: >).prefix(5))
}

（そしてForEachを、）
ForEach(
    Array(
        scores
            .sorted(by: >)
            .prefix(5)
            .enumerated()
    ),
    id: \.offset
) { index, score in

（から、こちらに変更します。）

ForEach(rankingScores.indices, id: \.self) { index in

    let score = rankingScores[index]

    HStack {

        Text("\(index + 1)")
            .font(.title2)
            .bold()
            .foregroundStyle(.white)
            .frame(width: 45, height: 45)
            .background(rankColor(index))
            .clipShape(Circle())

        Text("\(index + 1)位")
            .font(.headline)
            .bold()
            .foregroundStyle(.white)

        Spacer()

        Text("\(score)")
            .font(.title2)
            .bold()
            .foregroundStyle(.yellow)

        Text("点")
            .foregroundStyle(.white)
    }
    .padding()
    .background(Color.purple.opacity(0.75))
    .clipShape(RoundedRectangle(cornerRadius: 18))
}

（つまり、最初の部分はこうなります。）

struct RankingView: View {

    @State private var scores: [Int] = []

    // ランキング表示用
    var rankingScores: [Int] {
        Array(scores.sorted(by: >).prefix(5))
    }

    var body: some View {

        ZStack {
            // ここから画面
        }
    }
}

（なぜこれで直りやすいの？

元のコードではSwiftが一度に、）
scores
 ↓
sorted
 ↓
prefix
 ↓
enumerated
 ↓
Array
 ↓
ForEach
 ↓
indexとscoreの型を判断
 ↓
HStack
 ↓
大量のmodifier
（まで考える必要があります。

それを、）
var rankingScores: [Int] {
    Array(scores.sorted(by: >).prefix(5))
}
（と先に**「これは [Int] ですよ」**と確定させてあげることで、コンパイラの仕事がかなり簡単になります。

このエラーはSwiftUIではよくあります。

**「7行目が間違っている」ではなく、「7行目から始まる body が複雑すぎる」**と考えるのがポイントです。

もしよければ、今の希望である**「絵文字なし・背景色中心・ハロウィン風・可愛い・見やすい」を維持したまま、bodyを小さなViewに分割して、このエラーが出にくい完成版のRankingViewを最初から全部書き直す**のが一番確実です。）

#AIに聞いてみた

//

//  ContentView.swift

//  HalloweenMerge2

//

//  Created by cmStudent on 2026/10/19.

//

import SwiftUI

struct RankingView: View {

    @State private var scores: [Int] = []

    // ランキング表示用

    var rankingScores: [Int] {

        Array(scores.sorted(by: >).prefix(5))

    }

    var body: some View {

        ZStack {

            // 背景画像

            Image("halloweenBackground")

                .resizable()

                .scaledToFill()

                .ignoresSafeArea()

            // 背景を暗くして文字を読みやすくする

            Color.black

                .opacity(0.35)

                .ignoresSafeArea()

            VStack(spacing: 20) {

                // =========================

                // タイトル

                // =========================

                Text("SCORE RANKING")

                    .font(.system(size: 32, weight: .black))

                    .foregroundStyle(.white)

                    .padding(.horizontal, 30)

                    .padding(.vertical, 12)

                    .background(

                        Color.purple.opacity(0.85)

                    )

                    .clipShape(

                        RoundedRectangle(cornerRadius: 20)

                    )

                    .overlay(

                        RoundedRectangle(cornerRadius: 20)

                            .stroke(Color.orange, lineWidth: 3)

                    )

                    .shadow(

                        color: .black.opacity(0.4),

                        radius: 5,

                        y: 3

                    )

                // =========================

                // BEST SCORE

                // =========================

                VStack(spacing: 5) {

                    Text("BEST SCORE")

                        .font(.headline)

                        .bold()

                        .foregroundStyle(.purple)

                    Text("\(scores.max() ?? 0)")

                        .font(.system(size: 50, weight: .black))

                        .foregroundStyle(.orange)

                    Text("POINTS")

                        .font(.caption)

                        .bold()

                        .foregroundStyle(.purple.opacity(0.7))

                }

                .frame(maxWidth: .infinity)

                .padding(.vertical, 15)

                .background(

                    Color(red: 1.0, green: 0.92, blue: 0.72)

                )

                .clipShape(

                    RoundedRectangle(cornerRadius: 22)

                )

                .overlay(

                    RoundedRectangle(cornerRadius: 22)

                        .stroke(Color.orange, lineWidth: 3)

                )

                .shadow(

                    color: .black.opacity(0.3),

                    radius: 5,

                    y: 3

                )

                .padding(.horizontal, 25)

                // =========================

                // ランキング

                // =========================

                VStack(spacing: 10) {

                    ForEach(rankingScores.indices, id: \.self) { index in

                        let score = rankingScores[index]

                        HStack {

                            Text("\(index + 1)")

                                .font(.title2)

                                .bold()

                                .foregroundStyle(.white)

                                .frame(width: 45, height: 45)

                                .background(rankColor(index))

                                .clipShape(Circle())

                            Text("\(index + 1)位")

                                .font(.headline)

                                .bold()

                                .foregroundStyle(.white)

                            Spacer()

                            Text("\(score)")

                                .font(.title2)

                                .bold()

                                .foregroundStyle(.yellow)

                            Text("点")

                                .foregroundStyle(.white)

                        }

                        .padding()

                        .background(Color.purple.opacity(0.75))

                        .clipShape(RoundedRectangle(cornerRadius: 18))

                    }

                        HStack {

                            // 順位

                            Text("\(index + 1)")

                                .font(.title2)

                                .bold()

                                .foregroundStyle(.white)

                                .frame(width: 45, height: 45)

                                .background(

                                    rankColor(index)

                                )

                                .clipShape(Circle())

                            Text("\(index + 1)位")

                                .font(.headline)

                                .bold()

                                .foregroundStyle(.white)

                            Spacer()

                            // スコア

                            Text("\(score)")

                                .font(.title2)

                                .bold()

                                .foregroundStyle(.yellow)

                            Text("点")

                                .font(.subheadline)

                                .foregroundStyle(.white)

                        }

                        .padding(.horizontal, 15)

                        .padding(.vertical, 10)

                        .background(

                            Color.purple.opacity(0.75)

                        )

                        .clipShape(

                            RoundedRectangle(cornerRadius: 18)

                        )

                        .overlay(

                            RoundedRectangle(cornerRadius: 18)

                                .stroke(

                                    index == 0

                                        ? Color.orange

                                        : Color.white.opacity(0.25),

                                    lineWidth: index == 0 ? 3 : 1

                                )

                        )

                    }

                    // スコアがない場合

                    if scores.isEmpty {

                        Text("まだスコアがありません")

                            .font(.headline)

                            .foregroundStyle(.white)

                            .frame(maxWidth: .infinity)

                            .padding(.vertical, 30)

                    }

                }

                .padding(15)

                .background(

                    Color.black.opacity(0.6)

                )

                .clipShape(

                    RoundedRectangle(cornerRadius: 25)

                )

                .padding(.horizontal, 20)

                Spacer()

                // =========================

                // ホームボタン

                // =========================

                Button {

                    // ホーム画面へ戻る処理

                } label: {

                    Text("ホームへ戻る")

                        .font(.headline)

                        .bold()

                        .foregroundStyle(.white)

                        .frame(width: 180)

                        .padding(.vertical, 13)

                        .background(

                            Color.orange

                        )

                        .clipShape(

                            RoundedRectangle(cornerRadius: 18)

                        )

                        .shadow(

                            color: .black.opacity(0.4),

                            radius: 4,

                            y: 3

                        )

                }

                .padding(.bottom, 30)

            }

            .padding(.top, 30)

        }

        .onAppear {

            loadScores()

        }

    }

    // MARK: - スコア読み込み

    func loadScores() {

        scores = UserDefaults.standard.array(

            forKey: "scoreHistory"

        ) as? [Int] ?? []

    }

    // MARK: - 順位ごとの色

    func rankColor(_ index: Int) -> Color {

        if index == 0 {

            // 1位

            return Color.orange

        } else if index == 1 {

            // 2位

            return Color.purple.opacity(0.8)

        } else if index == 2 {

            // 3位

            return Color.brown.opacity(0.8)

        } else {

            // 4位・5位

            return Color.gray.opacity(0.7)

        }

    }

}

#Preview {

    RankingView()

}

(原因が分かりました。今のコードでは、ForEach の後に古いランキング表示用の HStack が残っています。

つまりランキングを表示するコードが二重になっています。しかも2つ目の HStack では、ForEach の外なのに index と score を使っているためエラーになります。

具体的には、ここまでは正しいです。)

ForEach(rankingScores.indices, id: \.self) { index in
    let score = rankingScores[index]

    HStack {
        // ...
    }
}

(ところが、その直後にもう一度、)

HStack {
    Text("\(index + 1)")
    // ...
    Text("\(score)")
}

(があります。この2つ目は丸ごと削除してください。

そのうえで、混乱しないように、今のコードを整理した完成版を下に載せます。いったん RankingView を全部これに置き換えてください。)

import SwiftUI

struct RankingView: View {

    @State private var scores: [Int] = []

    // 上位5件のスコア
    var rankingScores: [Int] {
        Array(scores.sorted(by: >).prefix(5))
    }

    var body: some View {

        ZStack {

            // 背景画像
            Image("halloweenBackground")
                .resizable()
                .scaledToFill()
                .ignoresSafeArea()

            // 背景を少し暗くする
            Color.black
                .opacity(0.35)
                .ignoresSafeArea()

            VStack(spacing: 20) {

                // =====================
                // タイトル
                // =====================

                Text("SCORE RANKING")
                    .font(.system(size: 32, weight: .black))
                    .foregroundStyle(.white)
                    .padding(.horizontal, 30)
                    .padding(.vertical, 12)
                    .background(Color.purple.opacity(0.85))
                    .clipShape(
                        RoundedRectangle(cornerRadius: 20)
                    )
                    .overlay(
                        RoundedRectangle(cornerRadius: 20)
                            .stroke(
                                Color.orange,
                                lineWidth: 3
                            )
                    )


                // =====================
                // BEST SCORE
                // =====================

                VStack(spacing: 5) {

                    Text("BEST SCORE")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.purple)

                    Text("\(scores.max() ?? 0)")
                        .font(
                            .system(
                                size: 50,
                                weight: .black
                            )
                        )
                        .foregroundStyle(.orange)

                    Text("POINTS")
                        .font(.caption)
                        .bold()
                        .foregroundStyle(.purple)
                }
                .frame(maxWidth: .infinity)
                .padding(.vertical, 15)
                .background(
                    Color(
                        red: 1.0,
                        green: 0.92,
                        blue: 0.72
                    )
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 22)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 22)
                        .stroke(
                            Color.orange,
                            lineWidth: 3
                        )
                )
                .padding(.horizontal, 25)


                // =====================
                // ランキング
                // =====================

                VStack(spacing: 10) {

                    ForEach(
                        rankingScores.indices,
                        id: \.self
                    ) { index in

                        let score = rankingScores[index]

                        HStack(spacing: 12) {

                            // 順位の丸
                            Text("\(index + 1)")
                                .font(.title2)
                                .bold()
                                .foregroundStyle(.white)
                                .frame(
                                    width: 45,
                                    height: 45
                                )
                                .background(
                                    rankColor(index)
                                )
                                .clipShape(Circle())

                            // 順位
                            Text("\(index + 1)位")
                                .font(.headline)
                                .bold()
                                .foregroundStyle(.white)

                            Spacer()

                            // スコア
                            Text("\(score)")
                                .font(.title2)
                                .bold()
                                .foregroundStyle(.yellow)

                            Text("点")
                                .font(.subheadline)
                                .foregroundStyle(.white)
                        }
                        .padding(.horizontal, 15)
                        .padding(.vertical, 10)
                        .background(
                            Color.purple.opacity(0.75)
                        )
                        .clipShape(
                            RoundedRectangle(
                                cornerRadius: 18
                            )
                        )
                    }


                    // スコアがない場合
                    if scores.isEmpty {

                        Text("まだスコアがありません")
                            .font(.headline)
                            .foregroundStyle(.white)
                            .frame(maxWidth: .infinity)
                            .padding(.vertical, 30)
                    }
                }
                .padding(15)
                .background(
                    Color.black.opacity(0.6)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 25)
                )
                .padding(.horizontal, 20)


                Spacer()


                // =====================
                // ホームボタン
                // =====================

                Button {

                    // ホーム画面へ戻る処理

                } label: {

                    Text("ホームへ戻る")
                        .font(.headline)
                        .bold()
                        .foregroundStyle(.white)
                        .frame(width: 180)
                        .padding(.vertical, 13)
                        .background(Color.orange)
                        .clipShape(
                            RoundedRectangle(
                                cornerRadius: 18
                            )
                        )
                }
                .padding(.bottom, 30)
            }
            .padding(.top, 30)
        }
        .onAppear {
            loadScores()
        }
    }


    // MARK: - スコア読み込み

    func loadScores() {

        scores = UserDefaults.standard.array(
            forKey: "scoreHistory"
        ) as? [Int] ?? []
    }


    // MARK: - 順位ごとの色

    func rankColor(_ index: Int) -> Color {

        if index == 0 {
            return .orange

        } else if index == 1 {
            return .purple

        } else if index == 2 {
            return .brown

        } else {
            return .gray
        }
    }
}


#Preview {
    RankingView()
}

(今回のポイントは、ForEach は1個だけにすることです。

構造としては、)

VStack
 │
 ├─ SCORE RANKING
 │
 ├─ BEST SCORE
 │
 ├─ VStack
 │    │
 │    └─ ForEach
 │         ├─ 1位
 │         ├─ 2位
 │         ├─ 3位
 │         ├─ 4位
 │         └─ 5位
 │
 └─ ホームへ戻る

 (となります。

また、今回の

The compiler is unable to type-check this expression in reasonable time

は、SwiftUIでは本当のエラー箇所ではなく var body: some View のところに表示されることがあるので、7行目だけを見ても原因が分かりにくかったわけです。

まず上の完成版に丸ごと置き換えてみてください。今回貼ってくれたコードにあった二重の HStack と、スコープ外の index・score は解消されています。)


#AIに聞いてみた
rankingViewにプラスして、スライドしたら今までの戦歴が全て表示されるようにプログラムを書いてください

#回答
（できます。今の RankingView に、横にスワイプすると「戦歴」画面へ切り替わるようにしましょう。

イメージは、）
← スワイプ →

┌──────────────────┐   ┌──────────────────┐
│  SCORE RANKING   │   │    SCORE HISTORY │
│                  │   │                  │
│  BEST  12580     │   │  1回目   3200点 │
│                  │ → │  2回目   5800点 │
│  1位  12580      │   │  3回目   2100点 │
│  2位  10240      │ ← │  4回目  12580点 │
│  3位   8950      │   │  5回目   6400点 │
└──────────────────┘   └──────────────────┘

（という形です。

SwiftUIでは TabView と .page を使うと、iPhoneのホーム画面のように左右スワイプで画面を切り替えられます。

今の RankingView を次のコードに置き換えてみてください。）

import SwiftUI

struct RankingView: View {

    @State private var scores: [Int] = []

    // 上位5件
    var rankingScores: [Int] {
        Array(scores.sorted(by: >).prefix(5))
    }

    var body: some View {

        ZStack {

            // =====================
            // 背景
            // =====================

            Image("halloweenBackground")
                .resizable()
                .scaledToFill()
                .ignoresSafeArea()

            Color.black
                .opacity(0.35)
                .ignoresSafeArea()


            // =====================
            // 横スワイプ
            // =====================

            TabView {

                // 1ページ目
                rankingPage

                // 2ページ目
                historyPage
            }
            .tabViewStyle(.page(indexDisplayMode: .always))
        }
        .onAppear {
            loadScores()
        }
    }


    // ==========================================
    // 1ページ目：ランキング
    // ==========================================

    var rankingPage: some View {

        VStack(spacing: 20) {

            // タイトル
            Text("SCORE RANKING")
                .font(.system(size: 32, weight: .black))
                .foregroundStyle(.white)
                .padding(.horizontal, 30)
                .padding(.vertical, 12)
                .background(
                    Color.purple.opacity(0.85)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 20)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 20)
                        .stroke(
                            Color.orange,
                            lineWidth: 3
                        )
                )


            // =====================
            // BEST SCORE
            // =====================

            VStack(spacing: 5) {

                Text("BEST SCORE")
                    .font(.headline)
                    .bold()
                    .foregroundStyle(.purple)

                Text("\(scores.max() ?? 0)")
                    .font(
                        .system(
                            size: 50,
                            weight: .black
                        )
                    )
                    .foregroundStyle(.orange)

                Text("POINTS")
                    .font(.caption)
                    .bold()
                    .foregroundStyle(.purple)
            }
            .frame(maxWidth: .infinity)
            .padding(.vertical, 15)
            .background(
                Color(
                    red: 1.0,
                    green: 0.92,
                    blue: 0.72
                )
            )
            .clipShape(
                RoundedRectangle(cornerRadius: 22)
            )
            .overlay(
                RoundedRectangle(cornerRadius: 22)
                    .stroke(
                        Color.orange,
                        lineWidth: 3
                    )
            )
            .padding(.horizontal, 25)


            // =====================
            // TOP 5
            // =====================

            VStack(spacing: 10) {

                ForEach(
                    rankingScores.indices,
                    id: \.self
                ) { index in

                    let score = rankingScores[index]

                    HStack(spacing: 12) {

                        // 順位
                        Text("\(index + 1)")
                            .font(.title2)
                            .bold()
                            .foregroundStyle(.white)
                            .frame(
                                width: 45,
                                height: 45
                            )
                            .background(
                                rankColor(index)
                            )
                            .clipShape(Circle())

                        Text("\(index + 1)位")
                            .font(.headline)
                            .bold()
                            .foregroundStyle(.white)

                        Spacer()

                        Text("\(score)")
                            .font(.title2)
                            .bold()
                            .foregroundStyle(.yellow)

                        Text("点")
                            .foregroundStyle(.white)
                    }
                    .padding(.horizontal, 15)
                    .padding(.vertical, 10)
                    .background(
                        Color.purple.opacity(0.75)
                    )
                    .clipShape(
                        RoundedRectangle(
                            cornerRadius: 18
                        )
                    )
                }


                if scores.isEmpty {

                    Text("まだスコアがありません")
                        .font(.headline)
                        .foregroundStyle(.white)
                        .frame(maxWidth: .infinity)
                        .padding(.vertical, 30)
                }
            }
            .padding(15)
            .background(
                Color.black.opacity(0.6)
            )
            .clipShape(
                RoundedRectangle(cornerRadius: 25)
            )
            .padding(.horizontal, 20)


            Spacer()


            Text("左にスワイプして戦歴を見る")
                .font(.caption)
                .foregroundStyle(.white.opacity(0.8))


            // ホームボタン
            Button {

                // ホーム画面へ戻る処理

            } label: {

                Text("ホームへ戻る")
                    .font(.headline)
                    .bold()
                    .foregroundStyle(.white)
                    .frame(width: 180)
                    .padding(.vertical, 13)
                    .background(Color.orange)
                    .clipShape(
                        RoundedRectangle(
                            cornerRadius: 18
                        )
                    )
            }
            .padding(.bottom, 30)
        }
        .padding(.top, 30)
    }


    // ==========================================
    // 2ページ目：今までの戦歴
    // ==========================================

    var historyPage: some View {

        VStack(spacing: 20) {

            // タイトル
            Text("SCORE HISTORY")
                .font(.system(size: 30, weight: .black))
                .foregroundStyle(.white)
                .padding(.horizontal, 30)
                .padding(.vertical, 12)
                .background(
                    Color.orange.opacity(0.9)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 20)
                )
                .overlay(
                    RoundedRectangle(cornerRadius: 20)
                        .stroke(
                            Color.purple,
                            lineWidth: 3
                        )
                )


            Text("今までの戦歴")
                .font(.title2)
                .bold()
                .foregroundStyle(.white)


            // =====================
            // 戦歴一覧
            // =====================

            if scores.isEmpty {

                Spacer()

                Text("まだ戦歴がありません")
                    .font(.headline)
                    .foregroundStyle(.white)

                Spacer()

            } else {

                ScrollView {

                    VStack(spacing: 10) {

                        ForEach(
                            Array(scores.enumerated()),
                            id: \.offset
                        ) { index, score in

                            HStack {

                                // プレイ回数
                                Text("\(index + 1)回目")
                                    .font(.headline)
                                    .bold()
                                    .foregroundStyle(.white)

                                Spacer()

                                // スコア
                                Text("\(score)")
                                    .font(.title3)
                                    .bold()
                                    .foregroundStyle(.yellow)

                                Text("点")
                                    .font(.subheadline)
                                    .foregroundStyle(.white)
                            }
                            .padding()
                            .background(
                                Color.purple.opacity(0.75)
                            )
                            .clipShape(
                                RoundedRectangle(
                                    cornerRadius: 15
                                )
                            )
                        }
                    }
                    .padding()
                }
                .background(
                    Color.black.opacity(0.55)
                )
                .clipShape(
                    RoundedRectangle(cornerRadius: 25)
                )
                .padding(.horizontal, 20)
            }


            Text("右にスワイプしてランキングへ戻る")
                .font(.caption)
                .foregroundStyle(.white.opacity(0.8))


            Button {

                // ホーム画面へ戻る処理

            } label: {

                Text("ホームへ戻る")
                    .font(.headline)
                    .bold()
                    .foregroundStyle(.white)
                    .frame(width: 180)
                    .padding(.vertical, 13)
                    .background(Color.orange)
                    .clipShape(
                        RoundedRectangle(
                            cornerRadius: 18
                        )
                    )
            }
            .padding(.bottom, 30)
        }
        .padding(.top, 30)
    }


    // ==========================================
    // スコア読み込み
    // ==========================================

    func loadScores() {

        scores = UserDefaults.standard.array(
            forKey: "scoreHistory"
        ) as? [Int] ?? []
    }


    // ==========================================
    // 順位の色
    // ==========================================

    func rankColor(_ index: Int) -> Color {

        if index == 0 {

            return .orange

        } else if index == 1 {

            return .purple

        } else if index == 2 {

            return .brown

        } else {

            return .gray
        }
    }
}


#Preview {
    RankingView()
}

（今回重要なのは、この部分です。）
TabView {

    rankingPage

    historyPage
}
.tabViewStyle(.page(indexDisplayMode: .always))

（TabView の中に、rankingPageと）
（
historyPageという2枚の画面を入れています。そのため、

ランキング → 左へスワイプ → 全戦歴

という動きになります。

そして戦歴側には、）
ScrollView {

（を入れてあります。たとえば100回ゲームをしても、）
1回目      3200点
2回目      5600点
3回目      2100点
4回目      8400点
5回目     12580点
   ↓
   ↓
100回目    7200点

（のように上下スクロールして全スコアを確認できます。

なお、今の saveScore() が）
var history = UserDefaults.standard.array(
    forKey: "scoreHistory"
) as? [Int] ?? []

history.append(score)

UserDefaults.standard.set(
    history,
    forKey: "scoreHistory"
)

（という保存方法なら、この RankingView の戦歴画面に過去に保存した全スコアがそのまま表示されます。

さらにゲームらしくするなら、次は戦歴を単なる「○回目・○点」ではなく、**「NEW RECORD」「最高得点の行だけオレンジ」「最新プレイを一番上」「プレイ日時も表示」**にすると完成度がかなり上がります。）

#AIに聞いてみた
仮のスコアを入れて画面かくにんをするにはどうしたらいいですか

@State private var scores: [Int] = []

#となっていますよね。これを一時的に、

@State private var scores: [Int] = [
    3200,
    5800,
    2100,
    12580,
    6400,
    8900,
    4300,
    10200,
    7500,
    3600,
    9200,
    5100
]

#に変えます。

#ただし、今のコードには、

.onAppear {
    loadScores()
}
(があります。これが実行されると、せっかく入れた仮スコアが UserDefaults のデータで上書きされます。

なので、画面確認中だけここをコメントアウトしてください。)
.onAppear {
    // loadScores()
}

(これでPreviewでもシミュレーターでも、)
BEST SCORE
12580

1位  12580点
2位  10200点
3位   9200点
4位   8900点
5位   7500点

(のようにランキングが表示されます。

さらに左にスワイプすると、戦歴画面には、)
1回目     3200点
2回目     5800点
3回目     2100点
4回目    12580点
5回目     6400点
...
12回目    5100点
(と表示され、上下スクロールの確認もできます。

画面確認が終わったら、必ず元に戻します。)

@State private var scores: [Int] = []

(そして)
.onAppear {
    loadScores()
}

（も元に戻してください。

もっとおすすめの方法

今後何度もデザイン確認するなら、#Preview のときだけ仮データを渡せるようにすると便利です。

例えば、）
struct RankingView: View {

    @State private var scores: [Int]

    init(scores: [Int] = []) {
        _scores = State(initialValue: scores)
    }
    （としておけば、）
    #Preview {
    RankingView(
        scores: [
            3200,
            5800,
            2100,
            12580,
            6400,
            8900,
            4300,
            10200
        ]
    )
}

（のように、本番の保存データを変更せずPreviewだけ仮スコアを表示できます。

ただ、今は授業のプロジェクトでコードを複雑にしない方がいいと思うので、まずは最初の方法）

@State private var scores: [Int] = [3200, 5800, 2100, 12580, ...]

ーーーー
.onAppear {
    // loadScores()
}
（で画面を確認するのが簡単です。）
#AIに聞いてみた
@State private var scores: [Int] = [ 3200, 5800, 2100, 12580, 6400, 8900, 4300, 10200, 7500, 3600, 9200, 5100 ] 　これは何行目ですか

#回答
(あなたが先ほど貼ってくれた RankingView では、struct RankingView: View { のすぐ下にあります。

現在はここです。)
struct RankingView: View {

    @State private var scores: [Int] = []

    // ランキング表示用
    var rankingScores: [Int] {
    (この)
    @State private var scores: [Int] = []
    （を削除して、仮スコアに置き換えます。）
    struct RankingView: View {

    // 仮のスコア
    @State private var scores: [Int] = [
        3200,
        5800,
        2100,
        12580,
        6400,
        8900,
        4300,
        10200,
        7500,
        3600,
        9200,
        5100
    ]

    // ランキング表示用
    var rankingScores: [Int] {
        Array(scores.sorted(by: >).prefix(5))
    }
    （あなたが貼ってくれたコードの行数で数えると、だいたい12行目付近です。

そして重要なのが、下のほうにある）
.onAppear {
    loadScores()
}
（を画面確認中だけ、）
.onAppear {
    // loadScores()
}
（にしてください。

そうしないと、仮スコアを入れても loadScores() によって上書きされてしまいます。）

#AIに聞いてみた

（貼り付けたドキュメント）
2は2が合体したら表示できるようにしてあるか

（確認しました。現状では「2と2を合体した瞬間に2を図鑑へ登録する」処理は、この CollectionView.swift だけでは入っていません。

図鑑側には discoverItem(_:) が用意されていて、値を受け取ると発見済みとして保存できます。

ただし現在、）

.compactMap { Int($0) } ?? [2]

（つまり ?? [2] を ?? [] にします。

そして、**ゲーム側の「2と2が合体した処理」**のところに、）
discoverItem(2)
（を入れる必要があります。

ただし、もっと良い方法があります。マージゲームなので、2だけ特別扱いするのではなく、）
discoverItem(2)
discoverItem(4)
discoverItem(8)
discoverItem(16)
...
（と個別に書くより、合体したときに自動的に図鑑登録する仕組みにした方がいいです。

例えばゲーム側で、）
let oldValue = 2
let newValue = oldValue * 2

discoverItem(oldValue)
discoverItem(newValue)
（とすれば）
2 + 2 → 4
（を作ったときに「2」と「4」を発見済みにできます。

ただ、あなたのゲーム側の「合体処理」が今どこに書かれているかが、このファイルには含まれていません。このファイルには図鑑画面と discoverItem() まではありますが、実際のマージ処理はありません。

ゲーム側の GameView.swift など、**「2と2を合体して4を作っているコード」**を貼ってもらえれば、そこを見て「この行の下にこれを入れる」と具体的に示せます。）










