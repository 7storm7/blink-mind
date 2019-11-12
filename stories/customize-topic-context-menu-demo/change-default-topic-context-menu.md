通过编写插件改变系统默认的📧context menu：删除edit menu 项，在第二个位置增加自定义项 
```javascript
function ChangeDefaultTopicContextMenuPlugin() {
  return {
    customizeTopicContextMenu(props, next) {
      let defaultMenus = next();
      console.log(defaultMenus);
      defaultMenus.splice(0, 1);
      console.log(defaultMenus);
      defaultMenus.splice(
        1,
        0,
        <MenuItem
          icon="group-objects"
          label="Shift + A"
          text="my customize menu"
          onClick={onClickMyMenu(props)}
        />
      );
      console.log(defaultMenus);
      return <>{defaultMenus}</>;
    }
  };
}

const changeDefaultContextMenuPlugins = [
  ChangeDefaultTopicContextMenuPlugin(),
  HotKeyPlugin()
];
export class ChangeDefaultTopicContextMenuDemo extends BaseDemo {
  renderDiagram() {
    return (
      <Diagram
        model={this.state.model}
        onChange={this.onChange}
        plugins={changeDefaultContextMenuPlugins}
      />
    );
  }
}
```