##The animations
Set up an animation system on each todos that appears. To do this we will need a package and therefore to install it on our project. We will cut the current nodeJs server to make a small command line:

``
npm install ReactCssTransition --save
``

Pour résumé, npm install pour dire que l'on install un package ReactCssTransition pour dire quel package --save, c'est pour l'ajouter automatiquement au fichier package.json qui répertorie tout les packages utilisé.

Pour utiliser ReactCssTransitionGroup, rien de plus simple, On doit importer la librairie et aussi un petit bout de css pour bien faire:

```JS
import ReactCSSTransitionGroup from 'react-addons-css-transition-group';
import '../animation.css';
```

```JS
<div className="messages">
    <ReactCSSTransitionGroup 
        component="div"
        className="message"
        transitionName="message"
        transitionEnterTimeout={200}
        transitionLeaveTimeout={200}
    >
        {messages} //boucle pour afficher des éléments comme la Todo.
    </ReactCSSTransitionGroup>
</div>
```

```CSS
/* ----------------------------
	ANIMATIONS
---------------------------- */

.message-enter {
	opacity: 0;
  transform: translateY(100%);
  transition: all 0.2s;
}

.message-enter-active {
	opacity: 1;
	transform: translateY(0);
}

.message-leave {
	opacity: 1;
  transform: translateY(0);
  transition: all 0.2s;
}

.message-leave-active {
	opacity: 0;
	transform: translateY(-100%);
}
```

For the rest it's just configuration... 😎
![Giphy](https://ressources.blogdumoderateur.com/2013/02/gif-anime.gif)