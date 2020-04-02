# Argparseについて

最初の数行
import argparse

from commands import list_tasks, add_task, done_task, clear_tasks

def main():
    *parser = argparse.ArgumentParser()*
    *sub_parsers = parser.add_subparsers()* > サブパーサーを追加

    list_parser = sub_parsers.add_parser('list', help="タスクの一覧を表示")　＞サブパーサーにパーサーを追加。
    list_parser.set_defaults(func=list_tasks)

    add_parser = sub_parsers.add_parser('add', help="タスクを追加")
    add_parser.add_argument('body', type=str, help="追加するタスクの本文")
    add_parser.set_defaults(func=add_task)

    done_parser = sub_parsers.add_parser('done', help="タスクを完了")
    done_parser.add_argument('body', type=str, help="完了にするタスクの本文")
    done_parser.set_defaults(func=done_task)

    clear_parser = sub_parsers.add_parser('clear', help="完了しているタスクを消去")
    clear_parser.set_defaults(func=clear_tasks)

    args = parser.parse_args()
    args.func(args)


if __name__ == "__main__":
    main()
